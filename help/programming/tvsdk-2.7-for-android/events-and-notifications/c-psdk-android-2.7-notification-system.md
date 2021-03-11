---
description: Gli oggetti MediaPlayerStatus forniscono informazioni sulle modifiche allo stato del lettore. Gli oggetti di notifica forniscono informazioni su avvisi ed errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore. Implementa listener di eventi per acquisire e rispondere agli eventi (oggetti MediaPlayerEvent).
title: Notifiche ed eventi per lo stato del lettore, l'attività, gli errori e la registrazione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---


# Notifiche ed eventi per lo stato del lettore, l&#39;attività, gli errori e la registrazione {#notifications-and-events-for-player-status-activity-errors-and-logging}

Eventi e notifiche consentono di gestire gli aspetti asincroni dell’applicazione video.

Gli oggetti MediaPlayerStatus forniscono informazioni sulle modifiche allo stato del lettore. Gli oggetti di notifica forniscono informazioni su avvisi ed errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore. Implementa listener di eventi per acquisire e rispondere agli eventi (oggetti MediaPlayerEvent).

L&#39;applicazione può recuperare le notifiche e le informazioni sullo stato. Utilizzando queste informazioni, puoi anche creare un sistema di registrazione per la diagnostica e la convalida.

## Contenuto della notifica {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` fornisce informazioni relative allo stato del lettore.

TVSDK fornisce un elenco cronologico delle notifiche `MediaPlayerNotification` e ogni notifica contiene le seguenti informazioni:

* Un timestamp
* Metadati diagnostici costituiti dai seguenti elementi:

   * `type`: INFORMAZIONI, AVVERTENZA o ERRORE.
   * `code`: Una rappresentazione numerica della notifica.
   * `name`: Una descrizione leggibile della notifica, ad esempio SEEK_ERROR
   * `metadata`: Coppie chiave/valore che contengono informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata `URL` fornisce un valore corrispondente a un URL correlato alla notifica.

   * `innerNotification`: Riferimento a un altro  `MediaPlayerNotification` oggetto che influisce direttamente su questa notifica.

Puoi archiviare queste informazioni localmente per analisi successive o inviarle a un server remoto per la registrazione e la rappresentazione grafica.

## Imposta il sistema di notifica {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

Puoi ascoltare le notifiche.

Il nucleo del sistema di notifica di Primetime Player è la classe `Notification` che rappresenta una notifica autonoma.

Per ricevere le notifiche, ascolta le notifiche come segue:

1. Implementa il callback `NotificationEventListener.onNotification()` .
1. TVSDK passa un oggetto `NotificationEvent` al callback.

   >[!NOTE]
   >
   >I tipi di notifiche sono enumerati nell&#39;enum `Notification.Type`:

   * `ERROR`
   * `INFO`
   * `WARNING`

## Aggiungere registrazione e debug in tempo reale {#section_9D4004308CB243AD9B50818895D10005}

Puoi utilizzare le notifiche per implementare la registrazione in tempo reale nella tua applicazione video.

Il sistema di notifica consente di raccogliere informazioni di registrazione e debug per scopi diagnostici e di convalida senza stress del sistema.

>[!IMPORTANT]
>
>Il back-end di registrazione non fa parte di una configurazione di produzione e non deve gestire il traffico ad alto carico. Se l’implementazione non deve essere completa, considera l’efficienza della trasmissione dei dati per evitare di sovraccaricare il sistema.

Ecco un esempio di come recuperare le notifiche:

1. Crea un thread di esecuzione basato su timer per l&#39;applicazione video che esegue periodicamente query sui dati raccolti dal sistema di notifica TVSDK.
1. Se l&#39;intervallo del timer è troppo grande e le dimensioni dell&#39;elenco eventi sono troppo piccole, l&#39;elenco degli eventi di notifica si sovrapporrà.

   >[!NOTE]
   >
   >Per evitare questo overflow, effettuare una delle seguenti operazioni:
   >
   >1. Diminuisce l&#39;intervallo di tempo che guida il thread che esegue il polling per i nuovi eventi.
   >1. Aumenta le dimensioni dell’elenco delle notifiche.


1. Serializza le voci dell&#39;evento di notifica più recenti in formato JSON e invia le voci a un server remoto per la post-elaborazione.

   >[!NOTE]
   >
   >Il server remoto può visualizzare graficamente i dati forniti in tempo reale.

1. Per rilevare la perdita degli eventi di notifica, cerca le lacune nella sequenza di valori di indice degli eventi.

