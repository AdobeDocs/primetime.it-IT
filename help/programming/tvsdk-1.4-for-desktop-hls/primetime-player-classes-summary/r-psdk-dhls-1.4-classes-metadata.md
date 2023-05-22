---
description: Queste classi forniscono metadati per pubblicità, spazi dei nomi e tracciamento.
title: Classi di metadati
exl-id: 4014b496-7fc4-4fa9-98da-28350668d35f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Classi di metadati {#metadata-classes}

Queste classi forniscono metadati per pubblicità, spazi dei nomi e tracciamento.

Pacchetto [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/package-detail.html)

| Nome | Descrizione |
|---|---|
| [AdSignalingMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AdSignalingMode.html) | Classe di enumerazione che espone le modalità di segnalazione supportate nella frase. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Classe che estende `Metadata` in particolare per Phrase. Fornisce le proprietà da configurare per la risoluzione degli annunci di frasi per un determinato elemento multimediale. Devi impostare tutte le proprietà richieste, tra cui l’ID zona, l’ID supporto e l’URL del server di annunci, per configurare il lettore in modo da risolvere correttamente gli annunci. |
| [ByteArrayMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/ByteArrayMetadata.html) | Obsoleto. Utilizzare `Metadata`. |
| [DefaultMetadataKeys](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/DefaultMetadataKeys.html) | Classe. |
| [Metadati](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/Metadata.html) | Definisce l’interfaccia generica per la configurazione di tutti i metadati disponibili per il lettore e per gli oggetti aggiuntivi. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Obsoleto. Utilizzare `Metadata`. |
| [Utilizzo metadati](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataUtils.html) | Classe di metodi per l&#39;utilizzo dei metadati. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Classe per la rappresentazione non elaborata dei metadati temporizzati inseriti in un flusso multimediale. |
| [TimedMetadataType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadataType.html) | Classe contenente i tipi supportati per i metadati temporizzati (nella playlist o nel flusso), ad esempio metadati ID3 o tag. |
