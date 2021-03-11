---
title: Aggiornamento dei metadati
description: Aggiornamento dei metadati
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Aggiornamento dei metadati{#upgrading-metadata}

Se un client DRM di Adobe Primetime rileva contenuti assemblati con Flash Media Rights Management Server 1.x, estrae i metadati di crittografia dal contenuto e li invia al server. Il server converte quindi i metadati FMRMS 1.x nel formato DRM di Primetime e li invia al client. Il client invia quindi i metadati aggiornati in una richiesta di licenza DRM standard di Primetime.

* La classe del gestore delle richieste è `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1MetadataHandler`.
* L&#39;URL della richiesta è &quot;*URL di base da 1.x content*&quot; +&quot; [!DNL /flashaccess/headerconversion/v1]&quot;.

La conversione dei metadati può essere effettuata al volo quando il server riceve i vecchi metadati dal client. In alternativa, il server potrebbe preelaborare il vecchio contenuto e memorizzare i metadati convertiti; in questo caso, quando il client richiede nuovi metadati, il server deve semplicemente recuperare i nuovi metadati che corrispondono all&#39;identificatore di licenza dei vecchi metadati.

Per convertire i metadati, il server deve eseguire le seguenti operazioni:

* Ottieni `LiveCycleKeyMetaData`. Per pre-convertire i metadati, `LiveCycleKeyMetaData` può essere ottenuto da un file in pacchetto 1.x utilizzando `MediaEncrypter.examineEncryptedContent()`. I metadati sono inclusi anche nella richiesta di conversione dei metadati ( `FMRMSv1MetadataHandler.getOriginalMetadata()`).

* Ottieni l&#39;identificatore di licenza dai vecchi metadati e trova la chiave di crittografia e i criteri DRM (queste informazioni erano originariamente nel database Adobe LiveCycle ES. Le politiche DRM del LiveCycle ES devono essere convertite in politiche DRM 2.0 di Primetime.) L&#39;implementazione di riferimento include script e codice di esempio per la conversione dei criteri DRM e l&#39;esportazione delle informazioni sulle licenze dal LiveCycle ES.
* Compila l&#39;oggetto `V2KeyParameters` (che recuperi chiamando `MediaEncrypter.getKeyParameters()`).

* Carica la `SigningCredential`, che è la credenziale del packager emessa da Adobe utilizzata per firmare i metadati di crittografia. Ottenere l&#39;oggetto `SignatureParameters` chiamando `MediaEncrypter.getSignatureParameters()` e compilare la credenziale di firma.

* Chiama `MetaDataConverter.convertMetadata()` per ottenere il `V2ContentMetaData`.

* Chiama `V2ContentMetaData.getBytes()` e archivia per un utilizzo futuro, oppure chiama `FMRMSv1MetadataHandler.setUpdatedMetadata()`.

