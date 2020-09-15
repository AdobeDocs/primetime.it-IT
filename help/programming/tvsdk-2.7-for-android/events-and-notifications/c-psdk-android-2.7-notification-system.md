---
description: Gli oggetti MediaPlayerStatus forniscono informazioni sulle modifiche nello stato del lettore. Gli oggetti di notifica forniscono informazioni sugli avvisi e gli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore. È possibile implementare i listener di eventi per acquisire e rispondere agli eventi (oggetti MediaPlayerEvent).
seo-description: Gli oggetti MediaPlayerStatus forniscono informazioni sulle modifiche nello stato del lettore. Gli oggetti di notifica forniscono informazioni sugli avvisi e gli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore. È possibile implementare i listener di eventi per acquisire e rispondere agli eventi (oggetti MediaPlayerEvent).
seo-title: Notifiche ed eventi per lo stato, l'attività, gli errori e la registrazione del lettore
title: Notifiche ed eventi per lo stato, l'attività, gli errori e la registrazione del lettore
uuid: ec840f14-38d1-4f43-b119-e1326515fc63
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# Notifiche ed eventi per lo stato, l&#39;attività, gli errori e la registrazione del lettore {#notifications-and-events-for-player-status-activity-errors-and-logging}

Eventi e notifiche consentono di gestire gli aspetti asincroni dell’applicazione video.

Gli oggetti MediaPlayerStatus forniscono informazioni sulle modifiche nello stato del lettore. Gli oggetti di notifica forniscono informazioni sugli avvisi e gli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore. È possibile implementare i listener di eventi per acquisire e rispondere agli eventi (oggetti MediaPlayerEvent).

L&#39;applicazione può recuperare le informazioni relative a notifica e stato. Utilizzando queste informazioni, potete anche creare un sistema di registrazione per la diagnostica e la convalida.

## Contenuto notifica {#section_DF951FF601794CF592841BB7406DC1A1}

`MediaPlayerNotification` fornisce informazioni relative allo stato del lettore.

TVSDK fornisce un elenco cronologico delle `MediaPlayerNotification` notifiche e ogni notifica contiene le informazioni seguenti:

* Timestamp
* Metadati diagnostici costituiti dai seguenti elementi:

   * `type`: INFORMAZIONI, AVVISI O ERRORI.
   * `code`: Una rappresentazione numerica della notifica.
   * `name`: Descrizione leggibile della notifica, ad esempio SEEK_ERROR
   * `metadata`: Coppie chiave/valore contenenti informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata `URL` fornisce un valore che è un URL correlato alla notifica.

   * `innerNotification`: Un riferimento a un altro `MediaPlayerNotification` oggetto che influisce direttamente su questa notifica.

Potete archiviare queste informazioni localmente per un&#39;analisi successiva o inviarle a un server remoto per la registrazione e la rappresentazione grafica.

## Configurare il sistema di notifica {#section_9E37C09ECFA54B3DA8D3AA9ED1BAFC17}

Potete ascoltare le notifiche.

Il nucleo del sistema di notifica Primetime Player è la `Notification` classe, che rappresenta una notifica standalone.

Per ricevere le notifiche, ascolta le notifiche nel modo seguente:

1. Implementa il `NotificationEventListener.onNotification()` callback.
1. TVSDK passa un `NotificationEvent` oggetto al callback.

   >[!NOTE]
   >
   >I tipi di notifiche sono enumerati nell&#39; `Notification.Type` enum:

   * `ERROR`
   * `INFO`
   * `WARNING`

## Aggiunta di registrazioni e debugging in tempo reale {#section_9D4004308CB243AD9B50818895D10005}

Potete utilizzare le notifiche per implementare la registrazione in tempo reale nell’applicazione video.

Il sistema di notifica consente di raccogliere le informazioni di registrazione e debug per la diagnostica e la convalida senza che sia necessario utilizzare il sistema.

>[!IMPORTANT]
>
>Il back-end di registrazione non fa parte di una configurazione di produzione e non deve gestire il traffico a carico elevato. Se non è necessario che l&#39;implementazione sia completa, considera l&#39;efficienza della trasmissione dei dati per evitare il sovraccarico del sistema.

Di seguito è riportato un esempio di come recuperare le notifiche:

1. Create un thread di esecuzione basato su timer per l’applicazione video che esegue periodicamente query sui dati raccolti dal sistema di notifica TVSDK.
1. Se l&#39;intervallo del timer è troppo grande e la dimensione dell&#39;elenco eventi è troppo piccola, l&#39;elenco degli eventi di notifica si estenda.

   >[!NOTE]
   >
   >Per evitare questo overflow, effettuare una delle seguenti operazioni:
   >
   >1. Diminuisce l&#39;intervallo di tempo che guida il thread che esegue il polling per i nuovi eventi.
   >1. Aumentate la dimensione dell&#39;elenco delle notifiche.


1. Serializzare le voci dell&#39;evento di notifica più recente in formato JSON e inviare le voci a un server remoto per la post-elaborazione.

   >[!NOTE]
   >
   >Il server remoto può visualizzare graficamente i dati forniti in tempo reale.

1. Per rilevare la perdita di eventi di notifica, cercate gli spazi vuoti nella sequenza di valori di indice dell&#39;evento.

