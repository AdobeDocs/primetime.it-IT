---
description: Gli oggetti MediaPlayerStatus forniscono informazioni sulle modifiche dello stato del lettore. Gli oggetti di notifica forniscono informazioni su avvisi ed errori. Gli errori che interrompono la riproduzione del video causano anche un cambiamento nello stato del lettore. È possibile implementare i listener di eventi per acquisire e rispondere agli eventi (oggetti MediaPlayerEvent).
title: Notifiche ed eventi per stato, attività, errori e registrazione del lettore
exl-id: c25e834e-ffa0-444c-9285-331e6841ac29
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# Notifiche ed eventi per stato, attività, errori e registrazione del lettore {#notifications-and-events-for-player-status-activity-errors-and-logging}

Eventi e notifiche consentono di gestire gli aspetti asincroni dell’applicazione video.

Gli oggetti MediaPlayerStatus forniscono informazioni sulle modifiche dello stato del lettore. Gli oggetti di notifica forniscono informazioni su avvisi ed errori. Gli errori che interrompono la riproduzione del video causano anche un cambiamento nello stato del lettore. È possibile implementare i listener di eventi per acquisire e rispondere agli eventi (oggetti MediaPlayerEvent).

L&#39;applicazione può recuperare le informazioni di notifica e stato. Utilizzando queste informazioni, puoi anche creare un sistema di registrazione per la diagnostica e la convalida.

## Contenuto della notifica {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` fornisce informazioni relative allo stato del lettore.

TVSDK fornisce un elenco cronologico di `MediaPlayerNotification` notifiche e ogni notifica contiene le seguenti informazioni:

* Una marca temporale
* Metadati diagnostici costituiti dai seguenti elementi:

   * `type`: INFO, WARN O ERROR.
   * `code`: rappresentazione numerica della notifica.
   * `name`: descrizione leggibile della notifica, ad esempio SEEK_ERROR
   * `metadata`: coppie chiave/valore contenenti informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata `URL` fornisce un valore che è un URL correlato alla notifica.

   * `innerNotification`: riferimento a un altro `MediaPlayerNotification` oggetto che influisce direttamente su questa notifica.

È possibile archiviare queste informazioni in locale per un&#39;analisi successiva o inviarle a un server remoto per la registrazione e la rappresentazione grafica.

## Configurare il sistema di notifica {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

Puoi ascoltare le notifiche.

Il nucleo del sistema di notifica del lettore Primetime è `Notification` che rappresenta una notifica autonoma.

Per ricevere le notifiche, ascolta le notifiche come segue:

1. Implementare `NotificationEventListener.onNotification()` callback.
1. TVSDK supera un `NotificationEvent` al callback.

   >[!NOTE]
   >
   >I tipi di notifica sono enumerati nel `Notification.Type` enum:

   * `ERROR`
   * `INFO`
   * `WARNING`

## Aggiungere registrazione in tempo reale e debug {#section_9D4004308CB243AD9B50818895D10005}

Puoi utilizzare le notifiche per implementare la registrazione in tempo reale nell’applicazione video.

Il sistema di notifica consente di raccogliere le informazioni di registrazione e debug per la diagnostica e la convalida senza dover sottoporre il sistema a stress.

>[!IMPORTANT]
>
>Il back-end di registrazione non fa parte di una configurazione di produzione e non è previsto che gestisca il traffico con carichi elevati. Se l’implementazione non deve essere assolutamente completa, considera l’efficienza della trasmissione dei dati per evitare di sovraccaricare il sistema.

Ecco un esempio di come recuperare le notifiche:

1. Crea un thread di esecuzione basato su timer per l’applicazione video che esegue periodicamente query sui dati raccolti dal sistema di notifica TVSDK.
1. Se l&#39;intervallo del timer è troppo grande e le dimensioni dell&#39;elenco eventi sono troppo piccole, l&#39;elenco eventi di notifica verrà sottoposto a overflow.

   >[!NOTE]
   >
   >Per evitare questo overflow, eseguire una delle operazioni seguenti:
   >
   >1. Diminuire l&#39;intervallo di tempo che guida il thread che esegue il polling per i nuovi eventi.
   >1. Aumenta le dimensioni dell’elenco di notifiche.


1. Serializza le voci più recenti dell’evento di notifica in formato JSON e invia le voci a un server remoto per la post-elaborazione.

   >[!NOTE]
   >
   >Il server remoto è in grado di visualizzare graficamente i dati forniti in tempo reale.

1. Per rilevare la perdita di eventi di notifica, cerca le lacune nella sequenza dei valori di indice degli eventi.
