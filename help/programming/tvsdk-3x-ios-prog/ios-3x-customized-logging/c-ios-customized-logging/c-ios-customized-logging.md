---
description: Puoi implementare un sistema di registrazione personalizzato.
title: Informazioni sulla registrazione personalizzata
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Registrazione personalizzata {#customized-logging}

Puoi implementare un sistema di registrazione personalizzato.

Oltre a eseguire la registrazione utilizzando notifiche predefinite, è possibile implementare un sistema di registrazione che utilizza i messaggi di registro e i messaggi generati da TVSDK. Per ulteriori informazioni sulle notifiche predefinite, consulta [Il sistema di notifica](https://help.adobe.com/en_US/primetime/psdk/ios/index.html#PSDKs-concept-The_Notification_System). Puoi utilizzare questi registri per risolvere eventuali problemi relativi alle applicazioni del lettore e per comprendere meglio il flusso di lavoro di riproduzione e pubblicità.

La registrazione personalizzata utilizza un’istanza singleton condivisa del `PSDKPTLogFactory`, che fornisce un meccanismo per registrare i messaggi su più logger. Puoi definire e aggiungere (registrare) uno o più logger alla `PTLogFactory`. Questo consente di definire più logger con implementazioni personalizzate, ad esempio un logger di console, un logger web o un logger di cronologia della console.

TVSDK genera messaggi di registro per molte delle sue attività, che `PTLogFactory` inoltra a tutti i logger registrati. L&#39;applicazione può inoltre generare messaggi di registro personalizzati, che vengono inoltrati a tutti i logger registrati. Ogni logger può filtrare i messaggi e intraprendere le azioni appropriate.

Esistono due implementazioni per `PTLogFactory`:

* Per l’ascolto dei registri.
* Per aggiungere registri a una `PTLogFactory`.

## Ascolta i registri {#listen-to-logs}

Per registrarsi per l’ascolto dei registri:
1. Implementare una classe personalizzata che segue il protocollo `PTLogger`:

   ```
   @implementation PTConsoleLogger 
   
   + (PTConsoleLogger *) consoleLogger { 
       return [[[PTConsoleLogger alloc] init] autorelease]; 
   } 
   
   - (void)logEntry:(PTLogEntry *)entry { 
       //Log the message to the console using NSLog  
       NSLog(@"[%@] %@", entry.tag, entry.message); 
   } 
   
   @end
   ```

1. Per registrare l&#39;istanza per la ricezione delle voci di registrazione, aggiungere un&#39;istanza di `PTLogger` al `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

Di seguito è riportato un esempio di filtro dei registri utilizzando `PTLogEntry` tipo:

```
@implementation PTConsoleLogger 
 
+ (PTConsoleLogger *) consoleLogger { 
    return [[[PTConsoleLogger alloc] init] autorelease]; 
} 
 
- (id) init { 
    self = [super init]; 
 
    if (self) { 
        self.logLevel = PTLogEntryTypeInfo; 
    } 
 
    return self; 
} 
 
- (void)logEntry:(PTLogEntry *) entry { 
    //Filtering the entry by log level  
    if (entry.type < _logLevel) { 
        return; 
    } 
 
    //Log the message to the console using NSLog NSLog(@"[%@] %@", entry.tag, entry.message); 
} 
 
@end
```

## Aggiungere nuovi messaggi di registro {#add-new-log-messages}

Per registrarsi e ascoltare i registri:

Crea un nuovo `PTLogEntry` e aggiungerlo a `thePTLogFactory`:

È possibile creare manualmente un&#39;istanza di `PTLogEntry` e aggiungerlo al `PTLogFactory` ha condiviso un&#39;istanza o utilizza una delle macro per eseguire la stessa attività.

Di seguito è riportato un esempio di registrazione tramite `PTLogDebug` macro:

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
