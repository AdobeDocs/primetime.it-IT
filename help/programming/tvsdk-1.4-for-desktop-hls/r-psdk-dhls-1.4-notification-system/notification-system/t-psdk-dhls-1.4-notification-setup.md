---
description: Puoi ascoltare le notifiche e aggiungere le tue notifiche alla cronologia delle notifiche.
title: Configurare il sistema di notifica
exl-id: da6cec2d-8488-4f61-881b-72999ece650c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
