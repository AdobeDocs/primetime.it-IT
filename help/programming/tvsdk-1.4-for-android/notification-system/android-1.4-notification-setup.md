---
description: Puoi ascoltare le notifiche e aggiungere le tue notifiche alla cronologia delle notifiche.
title: Configurare il sistema di notifica
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Configurare il sistema di notifica{#set-up-your-notification-system}

Puoi ascoltare le notifiche e aggiungere le tue notifiche alla cronologia delle notifiche.

Il nucleo del sistema di notifica del lettore Primetime è `Notification` che rappresenta una notifica autonoma.

Il `NotificationHistory` La classe fornisce un meccanismo per l&#39;accumulo di notifiche. Memorizza un registro di oggetti di notifica (NotificationHistoryItem) che rappresenta un insieme di notifiche.

Per ricevere le notifiche:

* Ascolta le notifiche
* Aggiungere notifiche alla cronologia delle notifiche

1. Ascolta le modifiche di stato.
1. Implementare `MediaPlayer.PlaybackEventListener.onStateChanged` callback.
1. TVSDK passa due parametri al callback:

   * Il nuovo stato ( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` oggetto

