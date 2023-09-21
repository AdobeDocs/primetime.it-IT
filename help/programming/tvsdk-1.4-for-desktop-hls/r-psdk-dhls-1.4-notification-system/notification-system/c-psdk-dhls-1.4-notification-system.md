---
description: Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche dello stato del lettore, avvisi ed errori. Gli errori che interrompono la riproduzione del video causano anche un cambiamento nello stato del lettore.
title: Notifiche per stato, attività, errori e registrazione del lettore
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Panoramica {#notifications-for-player-status-activity-errors-and-logging-overview}

Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche dello stato del lettore, avvisi ed errori. Gli errori che interrompono la riproduzione del video causano anche un cambiamento nello stato del lettore.

L&#39;applicazione può recuperare le informazioni sulla notifica e sullo stato. È inoltre possibile creare un sistema di registrazione per la diagnostica e la convalida utilizzando le informazioni di notifica.

Puoi implementare i listener di eventi per acquisire e rispondere agli eventi. Molti eventi forniscono `MediaPlayerNotification` notifiche di stato.
