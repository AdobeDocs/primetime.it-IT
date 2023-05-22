---
description: Queste classi forniscono metadati per pubblicità, spazi dei nomi e tracciamento.
title: Classi di metadati
exl-id: 3d98c5e1-6792-419b-9638-f156f1eafd1b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Classi di metadati{#metadata-classes}

Queste classi forniscono metadati per pubblicità, spazi dei nomi e tracciamento.

Pacchetto [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html)

| Nome | Descrizione |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | Classe che fornisce le proprietà che devono essere configurate per la risoluzione degli annunci per un determinato elemento multimediale. Tutte le proprietà richieste devono essere impostate in modo da configurare il lettore per la corretta risoluzione degli annunci. |
| AuditudeMetadata | Obsoleto. Utilizza AuditudeSettings. |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html) | Classe che estende Java `AdvertisingMetadata` in particolare per Phrase. Fornisce le proprietà da configurare per la risoluzione degli annunci di frasi per un determinato elemento multimediale. Devi impostare tutte le proprietà richieste, tra cui l’ID zona, l’ID supporto e l’URL del server di annunci, per configurare il lettore in modo da risolvere correttamente gli annunci. |
| [Metadati](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | Definisce l’interfaccia generica per la configurazione di tutti i metadati disponibili per il lettore e per gli oggetti aggiuntivi. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Classe generica simile alla struttura dati per la memorizzazione di coppie chiave-valore arbitrarie. |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Classe per la rappresentazione non elaborata dei metadati temporizzati inseriti in un flusso multimediale. |
