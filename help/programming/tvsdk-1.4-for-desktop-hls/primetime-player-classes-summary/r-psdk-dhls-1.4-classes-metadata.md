---
description: Queste classi forniscono metadati per annunci pubblicitari, namespace e tracciamento.
title: Classi di metadati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Classi di metadati {#metadata-classes}

Queste classi forniscono metadati per annunci pubblicitari, namespace e tracciamento.

Pacchetto: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/package-detail.html)

| Nome | Descrizione |
|---|---|
| [AdSignalingMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AdSignalingMode.html) | Classe di enumerazione che espone le modalità di segnalazione supportate nella frase. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Classe che estende `Metadata` in modo specifico per Phrase. Fornisce le proprietà da configurare per la risoluzione degli annunci relativi alla frase per un determinato elemento multimediale. Per configurare il lettore per la corretta risoluzione degli annunci, devi impostare tutte le proprietà richieste, inclusi l’ID zona, l’ID supporto e l’URL del server di annunci. |
| [ByteArrayMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/ByteArrayMetadata.html) | Obsoleto. Utilizza `Metadata`. |
| [ChiaviMetadatiPredefiniti](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/DefaultMetadataKeys.html) | Classe. |
| [Metadati](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/Metadata.html) | Definisce l&#39;interfaccia generica per configurare tutti i metadati disponibili per il lettore e gli oggetti aggiuntivi. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Obsoleto. Utilizza `Metadata`. |
| [MetadataUtils](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/MetadataUtils.html) | Classe di metodi per l&#39;utilizzo dei metadati. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Classe per la rappresentazione grezza dei metadati temporizzati inseriti in un flusso multimediale. |
| [TimedMetadataType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/metadata/TimedMetadataType.html) | Classe contenente i tipi supportati per i metadati temporizzati (nella playlist o nel flusso di lavoro), ad esempio i metadati ID3 o i tag. |