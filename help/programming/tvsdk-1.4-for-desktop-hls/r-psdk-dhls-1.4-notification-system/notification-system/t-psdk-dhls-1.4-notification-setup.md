---
description: Puoi ascoltare le notifiche e aggiungere le tue notifiche alla cronologia delle notifiche.
title: Configurare il sistema di notifica
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Configurare il sistema di notifica{#set-up-your-notification-system}

Puoi ascoltare le notifiche e aggiungere le tue notifiche alla cronologia delle notifiche.

Il nucleo del sistema di notifica di Primetime Player è la classe Notification, che rappresenta una notifica autonoma.

La classe NotificationHistory fornisce un meccanismo per l&#39;accumulo di notifiche. Memorizza un registro di notifica ( `NotificationHistoryItem`) che rappresenta un insieme di Notifiche.

Per ricevere le notifiche:

* Ascolta le notifiche
* Aggiungere notifiche alla cronologia delle notifiche

1. Ascolta le modifiche di stato.
1. Implementare `MediaPlayer.StatusChangeEvent.STATUS_CHANGED` listener di eventi.
1. TVSDK supera un `MediaPlayer.StatusChangeEvent` al listener di eventi, che contiene due parametri:

   * Il nuovo stato ( `MediaPlayer.Status`)
   * A `MediaPlayerNotification` oggetto
