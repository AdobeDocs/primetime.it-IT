---
description: Queste classi forniscono i metadati per la pubblicità, gli spazi dei nomi e il tracciamento.
seo-description: Queste classi forniscono i metadati per la pubblicità, gli spazi dei nomi e il tracciamento.
seo-title: Classi di metadati
title: Classi di metadati
uuid: 9cabd1b7-4343-41a1-a3e7-1b61235992db
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Classi di metadati {#metadata-classes}

Queste classi forniscono i metadati per la pubblicità, gli spazi dei nomi e il tracciamento.

| **Nome** | **Descrizione** |
|---|---|
| [PTAdMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdMetadata.html) | Classe che fornisce proprietà da configurare per la risoluzione degli annunci per un dato elemento multimediale. Tutte le proprietà richieste devono essere impostate per configurare il lettore per la risoluzione corretta degli annunci. |
| [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) | Classe che si estende `PTAdMetadata` specificamente per  ad Decioning Adobe Primetime. Fornisce le proprietà da configurare per la risoluzione  annunci Adobe Primetime e il processo decisionale per un dato elemento multimediale. Per configurare il lettore per la risoluzione degli annunci, devi impostare tutte le proprietà richieste, inclusi l&#39;ID di zona, l&#39;ID supporto e l&#39;URL del server degli annunci. |
| [PTMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMetadata.html) | Definisce la classe base per la configurazione di tutti i metadati disponibili per il lettore e gli oggetti aggiuntivi. |
| [PTTimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTimedMetadata.html) | Classe che rappresenta un tag HLS personalizzato nel flusso. |
| [PTTrackingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTrackingMetadata.html) | Definisce una classe base per tutti i metadati relativi al tracciamento e all&#39;analisi. |