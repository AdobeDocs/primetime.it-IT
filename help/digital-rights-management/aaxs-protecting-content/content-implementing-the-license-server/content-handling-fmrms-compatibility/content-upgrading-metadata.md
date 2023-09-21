---
title: Aggiornamento dei metadati
description: Aggiornamento dei metadati
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Aggiornamento dei metadati{#upgrading-metadata}

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
