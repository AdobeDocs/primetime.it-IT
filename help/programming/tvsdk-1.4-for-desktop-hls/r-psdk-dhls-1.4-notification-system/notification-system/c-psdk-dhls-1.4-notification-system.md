---
description: Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche allo stato del lettore, sugli avvisi e sugli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore.
seo-description: Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche allo stato del lettore, sugli avvisi e sugli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore.
seo-title: Notifiche per lo stato, l'attività, gli errori e la registrazione del lettore
title: Notifiche per lo stato, l'attività, gli errori e la registrazione del lettore
uuid: 7ce5bed0-f312-437e-a82f-b1d4a8e1926c
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Panoramica {#notifications-for-player-status-activity-errors-and-logging-overview}

Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche allo stato del lettore, sugli avvisi e sugli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore.

L&#39;applicazione può recuperare le informazioni relative alla notifica e allo stato. È inoltre possibile creare un sistema di registrazione per la diagnostica e la convalida utilizzando le informazioni di notifica.

È possibile implementare i listener di eventi per acquisire e rispondere agli eventi. Molti eventi forniscono notifiche di stato `MediaPlayerNotification`.