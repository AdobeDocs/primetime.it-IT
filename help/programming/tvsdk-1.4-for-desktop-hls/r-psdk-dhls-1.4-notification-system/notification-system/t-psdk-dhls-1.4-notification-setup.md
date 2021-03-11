---
description: Puoi ascoltare le notifiche e aggiungere le tue notifiche personalizzate alla cronologia delle notifiche.
title: Imposta il sistema di notifica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Imposta il sistema di notifica{#set-up-your-notification-system}

Puoi ascoltare le notifiche e aggiungere le tue notifiche personalizzate alla cronologia delle notifiche.

Il nucleo del sistema di notifica di Primetime Player è la classe Notification, che rappresenta una notifica autonoma.

La classe NotificationHistory fornisce un meccanismo per l&#39;accumulo di notifiche. Memorizza un registro di oggetti di notifica ( `NotificationHistoryItem`) che rappresenta una raccolta di Notifiche.

Per ricevere le notifiche:

* Ascoltare notifiche
* Aggiungi notifiche alla cronologia delle notifiche

1. Ascoltare le modifiche allo stato.
1. Implementa il listener di eventi `MediaPlayer.StatusChangeEvent.STATUS_CHANGED`.
1. TVSDK passa un&#39;istanza `MediaPlayer.StatusChangeEvent` al listener di eventi, che contiene due parametri:

   * Il nuovo stato ( `MediaPlayer.Status`)
   * Un oggetto `MediaPlayerNotification`

