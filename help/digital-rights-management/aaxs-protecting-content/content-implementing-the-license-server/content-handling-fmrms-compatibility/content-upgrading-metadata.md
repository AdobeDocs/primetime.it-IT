---
seo-title: Aggiornamento dei metadati
title: Aggiornamento dei metadati
uuid: cad0b23e-50ca-47ae-871f-be571cb00a26
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Aggiornamento dei metadati{#upgrading-metadata}

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

