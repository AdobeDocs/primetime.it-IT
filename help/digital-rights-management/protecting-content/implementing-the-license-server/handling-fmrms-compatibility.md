---
description: Gestione della compatibilità FMRMS
title: Aggiornamento dei client
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Gestione della compatibilità FMRMS {#handling-fmrms-compatibility}

Esistono due tipi di richieste relative alla compatibilità di Flash Media Rights Management Server 1.x. Un tipo di richiesta viene utilizzato per richiedere ai client 1.x di eseguire l&#39;aggiornamento a un runtime che supporta Adobe Primetime DRM 2.0 o versione successiva. Un altro viene utilizzato per aggiornare i metadati 1.x al formato DRM di Primetime prima che sia possibile richiedere una licenza. Il supporto per queste richieste è necessario solo se in precedenza è stato distribuito qualsiasi contenuto che utilizza FMRMS 1.0 o 1.5.

## Aggiornamento dei client {#upgrading-clients}

Se un client FMRMS 1.x contatta un server Adobe Primetime DRM, il server deve richiedere al client di eseguire l&#39;aggiornamento.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`.
* L’URL della richiesta è &quot;*URL di base da contenuto 1.x*&quot; + &quot; [!DNL /edcws/services/urn:EDCLicenseService]&quot;

  A differenza di altri gestori di richieste di Adobe Primetime, questo gestore non fornisce l’accesso ad alcuna informazione di richiesta o richiede l’impostazione di dati di risposta. Crea un&#39;istanza di `FMRMSv1RequestHandler`, quindi chiama `close()`

## Aggiornamento dei metadati {#upgrading-metadata}

Se un client di Access di Adobe rileva contenuti inclusi nel pacchetto con Flash Media Rights Management Server 1.x, estrae i metadati di crittografia dal contenuto e li invia al server. Il server convertirà i metadati FMRMS 1.x nel formato di accesso Adobe e li invierà nuovamente al client. Il client invia quindi i metadati aggiornati in una richiesta standard di licenza Adobe Access.

* La classe del gestore richieste è `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* L’URL della richiesta è &quot;*URL di base da contenuto 1.x*&quot; +&quot;/flashaccess/headerconversion/v1&quot;.

La conversione dei metadati può essere eseguita al volo quando il server riceve i metadati precedenti dal client. In alternativa, il server può pre-elaborare il contenuto precedente e archiviare i metadati convertiti; in questo caso, quando il client richiede nuovi metadati, il server deve solo recuperare i nuovi metadati che corrispondono all’identificatore di licenza dei metadati precedenti.

Per convertire i metadati, il server deve effettuare le seguenti operazioni:

* Ottenere `LiveCycleKeyMetaData`. Per preconvertire i metadati: `LiveCycleKeyMetaData` può essere ottenuto da un file in pacchetto 1.x utilizzando `MediaEncrypter.examineEncryptedContent()`. I metadati sono inclusi anche nella richiesta di conversione metadati ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).
* Ottenere l&#39;identificatore di licenza dai metadati precedenti e trovare la chiave e i criteri di crittografia (queste informazioni erano originariamente nel database di LiveCycle ES di Adobe. I criteri ES di LiveCycle devono essere convertiti in criteri Access 2.0 di Adobe.) L’implementazione di riferimento include script e codice di esempio per la conversione dei criteri e l’esportazione delle informazioni sulla licenza dal LiveCycle ES.
* Compila il `V2KeyParameters` oggetto (recuperato chiamando `MediaEncrypter.getKeyParameters()`).
* Carica `SigningCredential`, credenziale del packager rilasciata dall&#39;Adobe utilizzata per firmare i metadati di crittografia. Ottieni `SignatureParameters` oggetto chiamando `MediaEncrypter.getSignatureParameters()` e inserisci le credenziali di firma.
* Chiamata `MetaDataConverter.convertMetadata()` per ottenere `V2ContentMetaData`.
* Chiamata `V2ContentMetaData.getBytes()` e archiviare per un utilizzo futuro, o chiamare `FMRMSv1MetadataHandler.setUpdatedMetadata()`.
