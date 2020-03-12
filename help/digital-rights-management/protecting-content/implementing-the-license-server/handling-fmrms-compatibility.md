---
description: Gestione della compatibilità FMRMS
seo-description: Gestione della compatibilità FMRMS
seo-title: Aggiornamento dei client
title: Aggiornamento dei client
uuid: c32ee087-2edf-4d11-be36-e2b31f3769de
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

---


# Gestione della compatibilità FMRMS {#handling-fmrms-compatibility}

Esistono due tipi di richieste relative alla compatibilità di Flash Media Rights Management Server 1.x. Un tipo di richiesta viene utilizzato per richiedere ai client 1.x di eseguire l&#39;aggiornamento a un runtime che supporta Adobe Primetime DRM 2.0 o versione successiva. Un altro è utilizzato per aggiornare i metadati 1.x al formato DRM di Primetime prima che sia possibile richiedere una licenza. Il supporto per queste richieste è necessario solo se avete precedentemente distribuito contenuti che utilizzano FMRMS 1.0 o 1.5.

## Aggiornamento dei client {#upgrading-clients}

Se un client FMRMS 1.x contatta un server Adobe Primetime DRM, il server deve richiedere al client di effettuare l&#39;aggiornamento.

* La classe gestore di richieste è `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* L&#39;URL della richiesta è &quot;URL di *base dal contenuto* 1.x&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   A differenza di altri gestori di richieste Adobe Primetime, questo gestore non fornisce l&#39;accesso ad alcuna informazione di richiesta né richiede l&#39;impostazione di dati di risposta. Crea un’istanza del `FMRMSv1RequestHandler`, quindi chiama `close()`

## Aggiornamento dei metadati {#upgrading-metadata}

Se un client Adobe Access rileva contenuti inclusi in un pacchetto con Flash Media Rights Management Server 1.x, questi estrae i metadati di cifratura dal contenuto e li invia al server. Il server converte i metadati FMRMS 1.x nel formato Adobe Access e li rispedisce al client. Il client invia quindi i metadati aggiornati in una richiesta di licenza Adobe Access standard.

* La classe gestore di richieste è `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* L’URL della richiesta è &quot;URL di *base dal contenuto* 1.x&quot; +&quot;/flashaccess/headerconversion/v1&quot;.

La conversione dei metadati può essere effettuata al volo quando il server riceve i vecchi metadati dal client. In alternativa, il server potrebbe preelaborare il contenuto precedente e memorizzare i metadati convertiti; in questo caso, quando il client richiede nuovi metadati, il server deve semplicemente recuperare i nuovi metadati che corrispondono all&#39;identificatore di licenza dei vecchi metadati.

Per convertire i metadati, il server deve effettuare le seguenti operazioni:

* Vai `LiveCycleKeyMetaData`. Per pre-convertire i metadati, `LiveCycleKeyMetaData` è possibile ottenere da un file 1.x con pacchetto `MediaEncrypter.examineEncryptedContent()`. I metadati sono inclusi anche nella richiesta di conversione dei metadati ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).
* Ottenete l&#39;identificatore di licenza dai vecchi metadati, quindi individuate la chiave di crittografia e i criteri (queste informazioni erano originariamente presenti nel database Adobe LiveCycle ES. I criteri di LiveCycle ES devono essere convertiti nei criteri di Adobe Access 2.0.) L&#39;implementazione di riferimento include script e codice di esempio per la conversione dei criteri e l&#39;esportazione delle informazioni sulle licenze da LiveCycle ES.
* Compilare l&#39; `V2KeyParameters` oggetto (che si ottiene chiamando `MediaEncrypter.getKeyParameters()`).
* Caricate la credenziale del `SigningCredential`packager emessa da Adobe per firmare i metadati di cifratura. Ottenere l&#39; `SignatureParameters` oggetto chiamando `MediaEncrypter.getSignatureParameters()` e compilando la credenziale di firma.
* Chiamate `MetaDataConverter.convertMetadata()` per ottenere il `V2ContentMetaData`.
* Chiama `V2ContentMetaData.getBytes()` e archivia per un utilizzo futuro o chiama `FMRMSv1MetadataHandler.setUpdatedMetadata()`.