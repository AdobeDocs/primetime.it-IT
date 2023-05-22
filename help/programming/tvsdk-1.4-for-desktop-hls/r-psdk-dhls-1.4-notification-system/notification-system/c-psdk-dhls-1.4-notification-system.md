---
description: Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche dello stato del lettore, avvisi ed errori. Gli errori che interrompono la riproduzione del video causano anche un cambiamento nello stato del lettore.
title: Notifiche per stato, attività, errori e registrazione del lettore
exl-id: cce634aa-5394-46c0-a031-70d6fc1b754b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Panoramica {#notifications-for-player-status-activity-errors-and-logging-overview}

Gli oggetti MediaPlayerNotification forniscono informazioni sulle modifiche dello stato del lettore, avvisi ed errori. Gli errori che interrompono la riproduzione del video causano anche un cambiamento nello stato del lettore.

L&#39;applicazione può recuperare le informazioni sulla notifica e sullo stato. È inoltre possibile creare un sistema di registrazione per la diagnostica e la convalida utilizzando le informazioni di notifica.

Puoi implementare i listener di eventi per acquisire e rispondere agli eventi. Molti eventi forniscono `MediaPlayerNotification` notifiche di stato.
