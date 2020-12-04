---
description: Queste classi forniscono i metadati per la pubblicità, gli spazi dei nomi e il tracciamento.
seo-description: Queste classi forniscono i metadati per la pubblicità, gli spazi dei nomi e il tracciamento.
seo-title: Classi di metadati
title: Classi di metadati
uuid: 6d5099c8-d562-4635-9ef0-068cc6fb9f82
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---


# Classi di metadati{#metadata-classes}

Queste classi forniscono i metadati per la pubblicità, gli spazi dei nomi e il tracciamento.

Pacchetto: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| Nome | Descrizione |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | Classe che fornisce proprietà da configurare per la risoluzione degli annunci per un dato elemento multimediale. Tutte le proprietà richieste devono essere impostate per configurare il lettore per la risoluzione corretta degli annunci. |
| AuditudeMetadata | Obsoleto. Utilizzare AuditudeSettings. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Classe che estende Java `AdvertisingMetadata` specificamente per Phrase. Fornisce le proprietà da configurare per la risoluzione di Phrase ads per un dato elemento multimediale. Per configurare il lettore per la risoluzione degli annunci, devi impostare tutte le proprietà richieste, inclusi l&#39;ID di zona, l&#39;ID supporto e l&#39;URL del server degli annunci. |
| [Metadati](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | Definisce l&#39;interfaccia generica per configurare tutti i metadati disponibili per il lettore e gli oggetti aggiuntivi. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Classe generica simile alla struttura di dati per la memorizzazione di coppie chiave-valore arbitrarie. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Classe per la rappresentazione non elaborata dei metadati temporizzati inseriti in un flusso multimediale. |