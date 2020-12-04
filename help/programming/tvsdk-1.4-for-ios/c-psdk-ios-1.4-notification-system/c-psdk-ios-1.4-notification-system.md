---
description: Gli oggetti PTNotification forniscono informazioni sulle modifiche allo stato del lettore, agli avvisi e agli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore.
seo-description: Gli oggetti PTNotification forniscono informazioni sulle modifiche allo stato del lettore, agli avvisi e agli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore.
seo-title: Notifiche per lo stato del lettore, l'attività, gli errori e i registri
title: Notifiche per lo stato del lettore, l'attività, gli errori e i registri
uuid: 59716a66-3736-4076-8011-8104bfe3a83a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# Notifiche per stato del lettore, attività, errori e registrazione {#notifications-for-player-status-activity-errors-and-logs-overview}

Gli oggetti PTNotification forniscono informazioni sulle modifiche allo stato del lettore, agli avvisi e agli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore.

L&#39;applicazione può recuperare le informazioni relative alla notifica e allo stato. È inoltre possibile creare un sistema di registrazione per la diagnostica e la convalida utilizzando le informazioni di notifica.

>[!IMPORTANT]
>
>TVSDK utilizza anche *`notification`* per fare riferimento alle `NSNotifications` notifiche `PTMediaPlayer` *`event`*, inviate per fornire informazioni sull&#39;attività del lettore.

TVSDK inoltre rilascia `PTMediaPlayerNewNotificationItemEntryNotification` quando rilascia `PTNotification`.

È possibile implementare i listener di eventi per acquisire e rispondere agli eventi. Molti eventi forniscono notifiche di stato `PTNotification`.

## Contenuto notifica {#notification-content}

PTNotification fornisce informazioni correlate allo stato del lettore.

TVSDK fornisce un elenco cronologico delle notifiche `PTNotification`. Ogni notifica contiene le informazioni seguenti:

* Timestamp
* Metadati diagnostici costituiti dai seguenti elementi:

   * `type`: INFORMAZIONI, AVVISI O ERRORI.
   * `code`: Una rappresentazione numerica della notifica.
   * `name`: Descrizione leggibile della notifica, ad esempio SEEK_ERROR
   * `metadata`: Coppie chiave/valore contenenti informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata `URL` fornisce un valore che è un URL correlato alla notifica.

   * `innerNotification`: Un riferimento a un altro  `PTNotification` oggetto che influisce direttamente su questa notifica.

Potete archiviare queste informazioni localmente per un&#39;analisi successiva o inviarle a un server remoto per la registrazione e la rappresentazione grafica.

## Impostazione notifica {#notification-setup}

TVSDK imposta il lettore per le notifiche di base, anche se devi completare la stessa configurazione per le notifiche personalizzate.

Esistono due implementazioni per `PTNotification`:

* Per ascoltare
* Per aggiungere notifiche personalizzate a `PTNotificationHistory`

Per ascoltare le notifiche, TVSDK crea un&#39;istanza della classe `PTNotification` e la associa a un&#39;istanza della classe `PTMediaPlayerItem`, che è associata a un&#39;istanza PTMediaPlayer. Esiste una sola istanza `PTNotificationHistory` per `PTMediaPlayer`.

>[!IMPORTANT]
>
>Se state aggiungendo personalizzazioni, le applicazioni e non TVSDK devono eseguire tali passaggi.

## Ascolto delle notifiche {#listen-to-notifications}

Esistono due modi per ascoltare la notifica `PTNotification` nella cartella `PTMediaPlayer`:

1. Controllare manualmente la `PTNotificationHistory` del `PTMediaPlayerItem` con un timer e verificare le differenze:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Utilizzare la [NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) inserita del `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Effettuate la registrazione alla `NSNotification` utilizzando l&#39;istanza della `PTMediaPlayer` da cui desiderate ottenere le notifiche:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implementare le callback di notifica {#implement-notification-callbacks}

Potete implementare le callback di notifica.

1. Implementate il callback di notifica ottenendo la `PTNotification` dalle informazioni utente di `NSNotification` e leggendo i relativi valori utilizzando `PTMediaPlayerNotificationKey`:

   ```
   - (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
       PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
       NSLog(@"Notification: %@", notification); 
   }
   ```

## Aggiunta di notifiche personalizzate {#add-custom-notifications}

Per aggiungere una notifica personalizzata:
Create un nuovo `PTNotification` e aggiungetelo al `PTNotificationHistory` utilizzando il `PTMediaPlayerItem` corrente:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
