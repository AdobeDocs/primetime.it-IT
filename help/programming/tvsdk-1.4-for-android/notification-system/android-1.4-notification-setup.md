---
description: Potete ascoltare le notifiche e aggiungere notifiche personalizzate alla cronologia delle notifiche.
seo-description: Potete ascoltare le notifiche e aggiungere notifiche personalizzate alla cronologia delle notifiche.
seo-title: Configurare il sistema di notifica
title: Configurare il sistema di notifica
uuid: caa6a306-dea9-45ee-b0b3-569b5f2527a1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Configurare il sistema di notifica{#set-up-your-notification-system}

Potete ascoltare le notifiche e aggiungere notifiche personalizzate alla cronologia delle notifiche.

Il nucleo del sistema di notifica Primetime Player è la classe `Notification`, che rappresenta una notifica standalone.

La classe `NotificationHistory` fornisce un meccanismo per l&#39;accumulo di notifiche. Memorizza un registro di oggetti Notification (NotificationHistoryItem) che rappresenta un insieme di Notifiche.

Per ricevere le notifiche:

* Ascoltare le notifiche
* Aggiunta di notifiche alla cronologia delle notifiche

1. Ascoltare le modifiche allo stato.
1. Implementa il callback `MediaPlayer.PlaybackEventListener.onStateChanged`.
1. TVSDK passa due parametri al callback:

   * Il nuovo stato ( `MediaPlayer.PlayerState`)
   * Oggetto `MediaPlayerNotification`

