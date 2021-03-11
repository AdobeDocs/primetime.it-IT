---
description: MediaPlayerNotification fornisce informazioni relative allo stato del lettore.
title: Contenuto della notifica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Contenuto della notifica{#notification-content}

MediaPlayerNotification fornisce informazioni relative allo stato del lettore.

TVSDK fornisce un elenco cronologico delle notifiche `MediaPlayerNotification` . Ogni notifica contiene le seguenti informazioni:

* Timestamp
* Metadati diagnostici costituiti dai seguenti elementi:

   * digitare INFO, WARN o ERROR
   * `code`: Una rappresentazione numerica della notifica.
   * `name`: Una descrizione leggibile della notifica, ad esempio SEEK_ERROR
   * `metadata`: Coppie chiave/valore che contengono informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata `URL` fornisce un valore corrispondente a un URL correlato alla notifica.

   * `innerNotification`: Riferimento a un altro  `MediaPlayerNotification` oggetto che influisce direttamente su questa notifica.

Puoi archiviare queste informazioni localmente per analisi successive o inviarle a un server remoto per la registrazione e la rappresentazione grafica.
