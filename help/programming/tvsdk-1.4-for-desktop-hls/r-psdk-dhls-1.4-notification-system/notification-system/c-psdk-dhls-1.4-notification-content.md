---
description: MediaPlayerNotification fornisce informazioni relative allo stato del lettore.
title: Contenuto della notifica
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Contenuto della notifica{#notification-content}

MediaPlayerNotification fornisce informazioni relative allo stato del lettore.

TVSDK fornisce un elenco cronologico di `MediaPlayerNotification` notifiche. Ogni notifica contiene le seguenti informazioni:

* Timestamp
* Metadati diagnostici costituiti dai seguenti elementi:

   * digitare INFO, WARN o ERROR
   * `code`: rappresentazione numerica della notifica.
   * `name`: descrizione leggibile della notifica, ad esempio SEEK_ERROR
   * `metadata`: coppie chiave/valore contenenti informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata `URL` fornisce un valore che è un URL correlato alla notifica.

   * `innerNotification`: riferimento a un altro `MediaPlayerNotification` oggetto che influisce direttamente su questa notifica.

È possibile archiviare queste informazioni in locale per un&#39;analisi successiva o inviarle a un server remoto per la registrazione e la rappresentazione grafica.
