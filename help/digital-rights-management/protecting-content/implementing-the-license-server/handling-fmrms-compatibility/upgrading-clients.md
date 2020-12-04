---
description: Esistono due tipi di richieste correlate alla compatibilità di Flash Media Rights Management Server 1.x. Un tipo di richiesta viene utilizzato per richiedere ai client 1.x di eseguire l'aggiornamento a un runtime che supporta  Adobe Primetime DRM 2.0 o versione successiva. Un altro è utilizzato per aggiornare i metadati 1.x al formato DRM di Primetime prima che sia possibile richiedere una licenza. Il supporto per queste richieste è necessario solo se avete precedentemente distribuito contenuti che utilizzano FMRMS 1.0 o 1.5.
seo-description: Esistono due tipi di richieste correlate alla compatibilità di Flash Media Rights Management Server 1.x. Un tipo di richiesta viene utilizzato per richiedere ai client 1.x di eseguire l'aggiornamento a un runtime che supporta  Adobe Primetime DRM 2.0 o versione successiva. Un altro è utilizzato per aggiornare i metadati 1.x al formato DRM di Primetime prima che sia possibile richiedere una licenza. Il supporto per queste richieste è necessario solo se avete precedentemente distribuito contenuti che utilizzano FMRMS 1.0 o 1.5.
seo-title: Gestione della compatibilità FMRMS
title: Gestione della compatibilità FMRMS
uuid: c32ee087-2edf-4d11-be36-e2b31f3769de
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---


# Gestione della compatibilità FMRMS {#handling-fmrms-compatibility}

Esistono due tipi di richieste correlate alla compatibilità di Flash Media Rights Management Server 1.x. Un tipo di richiesta viene utilizzato per richiedere ai client 1.x di eseguire l&#39;aggiornamento a un runtime che supporta  Adobe Primetime DRM 2.0 o versione successiva. Un altro è utilizzato per aggiornare i metadati 1.x al formato DRM di Primetime prima che sia possibile richiedere una licenza. Il supporto per queste richieste è necessario solo se avete precedentemente distribuito contenuti che utilizzano FMRMS 1.0 o 1.5.

## Aggiornamento dei client {#upgrading-clients}

Se un client FMRMS 1.x contatta un server Adobe Primetime DRM , il server deve richiedere al client di eseguire l&#39;aggiornamento.

* La classe del gestore di richieste è `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* L&#39;URL della richiesta è &quot;*URL di base da 1.x content*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

   A differenza  altri gestori di richieste Adobe Primetime, questo gestore non fornisce l&#39;accesso alle informazioni di richiesta né richiede l&#39;impostazione di dati di risposta. Creare un&#39;istanza del `FMRMSv1RequestHandler`, quindi chiamare `close()`

## Aggiornamento dei metadati {#upgrading-metadata}

Se un client Adobe Primetime DRM  rileva contenuti inclusi in pacchetti con Flash Media Rights Management Server 1.x, estrae quindi i metadati di cifratura dal contenuto e li invia al server. Il server converte quindi i metadati FMRMS 1.x nel formato DRM di Primetime e li invia al client. Il client invia quindi i metadati aggiornati in una richiesta di licenza DRM standard di Primetime.

* La classe del gestore di richieste è `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* L&#39;URL della richiesta è &quot;*URL di base da 1.x content*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;.

La conversione dei metadati può essere effettuata al volo quando il server riceve i vecchi metadati dal client. In alternativa, il server potrebbe preelaborare il contenuto precedente e memorizzare i metadati convertiti; in questo caso, quando il client richiede nuovi metadati, il server deve semplicemente recuperare i nuovi metadati che corrispondono all&#39;identificatore di licenza dei vecchi metadati.

Per convertire i metadati, il server deve effettuare le seguenti operazioni:

* Get `LiveCycleKeyMetaData`. Per pre-convertire i metadati, `LiveCycleKeyMetaData` può essere ottenuto da un pacchetto di file 1.x utilizzando `MediaEncrypter.examineEncryptedContent()`. I metadati sono inclusi anche nella richiesta di conversione dei metadati ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).

* Ottenete l&#39;identificatore di licenza dai vecchi metadati, individuate la chiave di crittografia e i criteri DRM (queste informazioni erano originariamente presenti nel database ES del LiveCycle di Adobe  . I criteri DRM di LiveCycle ES devono essere convertiti in criteri DRM di Primetime DRM 2.0.) L&#39;implementazione di riferimento include script e codice di esempio per la conversione dei criteri DRM e l&#39;esportazione delle informazioni sulle licenze dal LiveCycle ES.
* Compilare l&#39;oggetto `V2KeyParameters` (che si ottiene chiamando `MediaEncrypter.getKeyParameters()`).

* Caricate la `SigningCredential`, ovvero la credenziale del packager emessa dal Adobe  utilizzato per firmare i metadati di cifratura. Ottenere l&#39;oggetto `SignatureParameters` chiamando `MediaEncrypter.getSignatureParameters()` e compilando la credenziale di firma.

* Chiamare `MetaDataConverter.convertMetadata()` per ottenere il `V2ContentMetaData`.

* Chiamare `V2ContentMetaData.getBytes()` e memorizzare per un utilizzo futuro oppure chiamare `FMRMSv1MetadataHandler.setUpdatedMetadata()`.