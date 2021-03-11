---
description: Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche allo stato del lettore, sugli avvisi e sugli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore.
title: Notifiche relative allo stato, all’attività, agli errori e alla registrazione del lettore
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# Panoramica {#notifications-for-player-status-activity-errors-and-logging-overview}

Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche allo stato del lettore, sugli avvisi e sugli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore.

L&#39;applicazione può recuperare le informazioni relative alla notifica e allo stato. È inoltre possibile creare un sistema di registrazione per la diagnostica e la convalida utilizzando le informazioni di notifica.

Implementa listener di eventi per acquisire e rispondere agli eventi. Molti eventi forniscono notifiche di stato `MediaPlayerNotification`.