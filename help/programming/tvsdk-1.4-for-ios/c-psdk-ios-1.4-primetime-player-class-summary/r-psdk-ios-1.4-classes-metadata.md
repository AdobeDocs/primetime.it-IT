---
description: Queste classi forniscono metadati per pubblicità, spazi dei nomi e tracciamento.
title: Classi di metadati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Classi di metadati{#metadata-classes}

Queste classi forniscono metadati per pubblicità, spazi dei nomi e tracciamento.

| Nome | Descrizione |
|---|---|
| [PTAdMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdMetadata.html) | Classe che fornisce le proprietà che devono essere configurate per la risoluzione degli annunci per un determinato elemento multimediale. Tutte le proprietà richieste devono essere impostate in modo da configurare il lettore per la corretta risoluzione degli annunci. |
| [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) | Classe che estende `PTAdMetadata` in particolare per Adobe Primetime ad decisioning. Fornisce le proprietà da configurare per la risoluzione degli annunci di Adobe Primetime Ad Decisioning per un determinato elemento multimediale. Devi impostare tutte le proprietà richieste, tra cui l’ID zona, l’ID supporto e l’URL del server di annunci, per configurare il lettore in modo da risolvere correttamente gli annunci. |
| [PTMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMetadata.html) | Definisce la classe base per la configurazione di tutti i metadati disponibili per il lettore e per gli oggetti aggiuntivi. |
| [PTTimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTimedMetadata.html) | Classe che rappresenta un tag HLS personalizzato nel flusso. |
| [PTTrackingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTrackingMetadata.html) | Definisce una classe base per tutti i metadati relativi al tracciamento e all’analisi. |
