---
description: Gli oggetti PTNotification forniscono informazioni sulle modifiche dello stato del lettore, avvisi ed errori. Gli errori che interrompono la riproduzione del video causano anche un cambiamento nello stato del lettore.
title: Contenuto della notifica
exl-id: 62423718-b154-4105-82b2-f6e389105ec8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# Notifiche per stato, attività, errori e registrazione del lettore {#notifications-player-status-activity-errors-logging}

`PTNotification` Gli oggetti forniscono informazioni sulle modifiche dello stato del lettore, avvisi ed errori. Gli errori che interrompono la riproduzione del video causano anche un cambiamento nello stato del lettore.

L&#39;applicazione può recuperare le informazioni sulla notifica e sullo stato. È inoltre possibile creare un sistema di registrazione per la diagnostica e la convalida utilizzando le informazioni di notifica.

>[!NOTE]
>
>TVSDK utilizza anche *`notification`* per fare riferimento `NSNotifications` ( `PTMediaPlayer` notifiche) *`event`* notifiche, inviate per fornire informazioni sull’attività del lettore.

Problemi relativi anche a TVSDK `PTMediaPlayerNewNotificationItemEntryNotification` quando si verificano problemi `PTNotification`.

Puoi implementare i listener di eventi per acquisire e rispondere agli eventi. Molti eventi forniscono `PTNotification` notifiche di stato.

## Contenuto della notifica {#notification-content}

`PTNotification` fornisce informazioni relative allo stato del lettore.

TVSDK fornisce un elenco cronologico di `PTNotification` notifiche. Ogni notifica contiene le seguenti informazioni:

* Timestamp
* Metadati diagnostici costituiti dai seguenti elementi:

   * `type`: INFO, WARN O ERROR.
   * `code`: rappresentazione numerica della notifica.
   * `name`: descrizione leggibile della notifica, ad esempio SEEK_ERROR
   * `metadata`: coppie chiave/valore contenenti informazioni rilevanti sulla notifica. Ad esempio, una chiave denominata `URL` fornisce un valore che è un URL correlato alla notifica.

   * `innerNotification`: riferimento a un altro `PTNotification` oggetto che influisce direttamente su questa notifica.

È possibile archiviare queste informazioni in locale per un&#39;analisi successiva o inviarle a un server remoto per la registrazione e la rappresentazione grafica.

## Configurazione delle notifiche {#notification-setup}

TVSDK imposta il lettore per le notifiche di base, anche se è necessario completare la stessa configurazione per le notifiche personalizzate.

Esistono due implementazioni per `PTNotification`:

* Per ascoltare
* Per aggiungere notifiche personalizzate `PTNotificationHistory`

Per ascoltare le notifiche, TVSDK crea un&#39;istanza del `PTNotification` e la collega a un&#39;istanza della classe `PTMediaPlayerItem`, collegato a un&#39;istanza PTMediaPlayer. Ce n&#39;è solo uno `PTNotificationHistory` istanza per `PTMediaPlayer`.

>[!IMPORTANT]
>
>Se stai aggiungendo personalizzazioni, le applicazioni e non TVSDK, devono eseguire questi passaggi.

## Ascolta le notifiche {#listen-to-notifications}

Esistono due modi per ascoltare `PTNotification` notifica in `PTMediaPlayer`:

1. Controlla manualmente il `PTNotificationHistory` del `PTMediaPlayerItem` con un timer e verifica le differenze:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Utilizza il pubblicato [NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) del `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Registrati al `NSNotification` utilizzando l&#39;istanza di `PTMediaPlayer` da cui desideri ricevere le notifiche:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implementare i callback di notifica {#implement-notification-callbacks}

Puoi implementare i callback di notifica.

Implementa il callback di notifica ottenendo `PTNotification` dal `NSNotification` informazioni utente e lettura dei relativi valori tramite `PTMediaPlayerNotificationKey`:

```
- (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
    PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
    NSLog(@"Notification: %@", notification); 
}
```

## Aggiungere notifiche personalizzate {#add-custom-notifications}

Per aggiungere una notifica personalizzata: crea un nuovo `PTNotification` e aggiungerlo al `PTNotificationHistory` utilizzando il `PTMediaPlayerItem`:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
