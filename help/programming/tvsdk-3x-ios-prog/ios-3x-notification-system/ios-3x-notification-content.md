---
description: Gli oggetti PTNotification forniscono informazioni sulle modifiche allo stato del lettore, sugli avvisi e sugli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore.
title: Contenuto della notifica
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Notifiche relative allo stato, all&#39;attività, agli errori e alla registrazione del lettore {#notifications-player-status-activity-errors-logging}

`PTNotification` Gli oggetti forniscono informazioni sulle modifiche dello stato del lettore, sugli avvisi e sugli errori. Gli errori che arrestano la riproduzione del video provocano anche una modifica dello stato del lettore.

L&#39;applicazione può recuperare le informazioni relative alla notifica e allo stato. È inoltre possibile creare un sistema di registrazione per la diagnostica e la convalida utilizzando le informazioni di notifica.

>[!NOTE]
>
>TVSDK utilizza anche le notifiche *`notification`* per fare riferimento a `NSNotifications` ( `PTMediaPlayer` notifiche) *`event`* inviate per fornire informazioni sull’attività del lettore.

Anche TVSDK rilascia `PTMediaPlayerNewNotificationItemEntryNotification` quando si verifica un problema `PTNotification`.

Implementa listener di eventi per acquisire e rispondere agli eventi. Molti eventi forniscono notifiche di stato `PTNotification`.

## Contenuto della notifica {#notification-content}

`PTNotification` fornisce informazioni relative allo stato del lettore.

TVSDK fornisce un elenco cronologico delle notifiche `PTNotification` . Ogni notifica contiene le seguenti informazioni:

* Timestamp
* Metadati diagnostici costituiti dai seguenti elementi:

   * `type`: INFORMAZIONI, AVVERTENZA o ERRORE.
   * `code`: Una rappresentazione numerica della notifica.
   * `name`: Una descrizione leggibile della notifica, ad esempio SEEK_ERROR
   * `metadata`: Coppie chiave/valore che contengono informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata `URL` fornisce un valore corrispondente a un URL correlato alla notifica.

   * `innerNotification`: Riferimento a un altro  `PTNotification` oggetto che influisce direttamente su questa notifica.

Puoi archiviare queste informazioni localmente per analisi successive o inviarle a un server remoto per la registrazione e la rappresentazione grafica.

## Configurazione delle notifiche {#notification-setup}

TVSDK imposta il lettore per le notifiche di base, anche se devi completare la stessa configurazione per le notifiche personalizzate.

Sono disponibili due implementazioni per `PTNotification`:

* Ascoltare
* Per aggiungere notifiche personalizzate a `PTNotificationHistory`

Per ascoltare le notifiche, TVSDK crea un&#39;istanza della classe `PTNotification` e la associa a un&#39;istanza del `PTMediaPlayerItem`, che è associata a un&#39;istanza PTMediaPlayer. Esiste una sola istanza `PTNotificationHistory` per `PTMediaPlayer`.

>[!IMPORTANT]
>
>Se stai aggiungendo personalizzazioni, le applicazioni e non TVSDK, devono eseguire questi passaggi.

## Ascolta le notifiche {#listen-to-notifications}

Ci sono due modi per ascoltare la notifica `PTNotification` nel `PTMediaPlayer`:

1. Controllare manualmente il `PTNotificationHistory` del `PTMediaPlayerItem` con un timer e controllare le differenze:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Utilizza il [NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) inviato del `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Registrati al `NSNotification` utilizzando l&#39;istanza del `PTMediaPlayer` da cui desideri ottenere le notifiche:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implementare i callback di notifica {#implement-notification-callbacks}

Puoi implementare i callback di notifica.

Implementa il callback di notifica ottenendo il `PTNotification` dalle informazioni utente `NSNotification` e leggendo i relativi valori utilizzando `PTMediaPlayerNotificationKey`:

```
- (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
    PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
    NSLog(@"Notification: %@", notification); 
}
```

## Aggiungi notifiche personalizzate {#add-custom-notifications}

Per aggiungere una notifica personalizzata:
Crea un nuovo `PTNotification` e aggiungilo al `PTNotificationHistory` utilizzando il `PTMediaPlayerItem` corrente:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
