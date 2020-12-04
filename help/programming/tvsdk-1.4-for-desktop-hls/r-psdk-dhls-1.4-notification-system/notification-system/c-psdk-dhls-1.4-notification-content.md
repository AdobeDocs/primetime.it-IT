---
description: MediaPlayerNotification fornisce informazioni correlate allo stato del lettore.
seo-description: MediaPlayerNotification fornisce informazioni correlate allo stato del lettore.
seo-title: Contenuto notifica
title: Contenuto notifica
uuid: c2321a49-1b60-4e44-b8e2-a023b764d779
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Contenuto notifica{#notification-content}

MediaPlayerNotification fornisce informazioni correlate allo stato del lettore.

TVSDK fornisce un elenco cronologico delle notifiche `MediaPlayerNotification`. Ogni notifica contiene le informazioni seguenti:

* Timestamp
* Metadati diagnostici costituiti dai seguenti elementi:

   * digitare INFO, AVVERTENZA o ERRORE
   * `code`: Una rappresentazione numerica della notifica.
   * `name`: Descrizione leggibile della notifica, ad esempio SEEK_ERROR
   * `metadata`: Coppie chiave/valore contenenti informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata `URL` fornisce un valore che è un URL correlato alla notifica.

   * `innerNotification`: Un riferimento a un altro  `MediaPlayerNotification` oggetto che influisce direttamente su questa notifica.

Potete archiviare queste informazioni localmente per un&#39;analisi successiva o inviarle a un server remoto per la registrazione e la rappresentazione grafica.
