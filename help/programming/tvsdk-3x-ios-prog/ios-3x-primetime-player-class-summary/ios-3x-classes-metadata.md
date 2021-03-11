---
description: Queste classi forniscono metadati per annunci pubblicitari, namespace e tracciamento.
title: Classi di metadati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# Classi di metadati {#metadata-classes}

Queste classi forniscono metadati per annunci pubblicitari, namespace e tracciamento.

| **Nome** | **Descrizione** |
|---|---|
| [PTAdMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdMetadata.html) | Classe che fornisce proprietà che devono essere configurate per la risoluzione degli annunci per un dato elemento multimediale. Tutte le proprietà richieste devono essere impostate per configurare il lettore per la corretta risoluzione degli annunci. |
| [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) | Classe che si estende `PTAdMetadata` in modo specifico per Adobe Primetime ad Decioning. Fornisce le proprietà da configurare per la risoluzione degli annunci Adobe Primetime e decisioning per un dato elemento multimediale. Per configurare il lettore per la corretta risoluzione degli annunci, devi impostare tutte le proprietà richieste, inclusi l’ID zona, l’ID supporto e l’URL del server di annunci. |
| [PTMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMetadata.html) | Definisce la classe base per la configurazione di tutti i metadati disponibili per il lettore e di oggetti aggiuntivi. |
| [PTTimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTimedMetadata.html) | Classe che rappresenta un tag HLS personalizzato nel flusso. |
| [PTTrackingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTrackingMetadata.html) | Definisce una classe base per tutti i metadati relativi al tracciamento e all&#39;analisi. |