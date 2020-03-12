---
description: Potete ascoltare le notifiche e aggiungere notifiche personalizzate alla cronologia delle notifiche.
seo-description: Potete ascoltare le notifiche e aggiungere notifiche personalizzate alla cronologia delle notifiche.
seo-title: Configurare il sistema di notifica
title: Configurare il sistema di notifica
uuid: 2d1876c7-4ce6-491c-880b-dd94697d4feb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Configurare il sistema di notifica{#set-up-your-notification-system}

Potete ascoltare le notifiche e aggiungere notifiche personalizzate alla cronologia delle notifiche.

Il nucleo del sistema di notifica Primetime Player è la classe Notification, che rappresenta una notifica standalone.

La classe NotificationHistory fornisce un meccanismo per l&#39;accumulo di notifiche. Memorizza un registro di oggetti notifica ( `NotificationHistoryItem`) che rappresenta una raccolta di Notifiche.

Per ricevere le notifiche:

* Ascoltare le notifiche
* Aggiunta di notifiche alla cronologia delle notifiche

1. Ascoltare le modifiche allo stato.
1. Implementare il listener di `MediaPlayer.StatusChangeEvent.STATUS_CHANGED` eventi.
1. TVSDK passa un&#39; `MediaPlayer.StatusChangeEvent` istanza al listener di eventi, che contiene due parametri:

   * Nuovo stato ( `MediaPlayer.Status`)
   * Un `MediaPlayerNotification` oggetto

