---
description: Queste classi forniscono metadati per annunci pubblicitari, namespace e tracciamento.
title: Classi di metadati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Classi di metadati{#metadata-classes}

Queste classi forniscono metadati per annunci pubblicitari, namespace e tracciamento.

Pacchetto: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| Nome | Descrizione |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | Classe che fornisce proprietà che devono essere configurate per la risoluzione degli annunci per un dato elemento multimediale. Tutte le proprietà richieste devono essere impostate per configurare il lettore per la corretta risoluzione degli annunci. |
| AuditudeMetadata | Obsoleto. Utilizza AuditudeSettings. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Classe che estende Java `AdvertisingMetadata` in modo specifico per Phrase. Fornisce le proprietà da configurare per la risoluzione degli annunci relativi alla frase per un determinato elemento multimediale. Per configurare il lettore per la corretta risoluzione degli annunci, devi impostare tutte le proprietà richieste, inclusi l’ID zona, l’ID supporto e l’URL del server di annunci. |
| [Metadati](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | Definisce l&#39;interfaccia generica per configurare tutti i metadati disponibili per il lettore e gli oggetti aggiuntivi. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Classe generica simile alla struttura dei dati per l&#39;archiviazione di coppie chiave-valore arbitrarie. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Classe per la rappresentazione grezza dei metadati temporizzati inseriti in un flusso multimediale. |