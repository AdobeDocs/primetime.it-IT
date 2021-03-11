---
description: Puoi implementare un tuo sistema di registrazione.
title: Registrazione personalizzata
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Registrazione personalizzata {#customized-logging}

Puoi implementare un tuo sistema di registrazione.

Oltre a registrare utilizzando notifiche predefinite, puoi implementare un sistema di registrazione che utilizza i messaggi di log e i messaggi generati da TVSDK. Per ulteriori informazioni sulle notifiche predefinite, vedere [Sistema di notifica](../c-psdk-ios-1.4-notification-system/c-psdk-ios-1.4-notification-system.md). È possibile utilizzare questi registri per risolvere i problemi delle applicazioni del lettore e per fornire una migliore comprensione del flusso di lavoro di riproduzione e pubblicità.

La registrazione personalizzata utilizza un&#39;istanza singleton condivisa di `PSDKPTLogFactory`, che fornisce un meccanismo per registrare i messaggi a più logger. Puoi definire e aggiungere (registrare) uno o più logger al `PTLogFactory`. Questo consente di definire più logger con implementazioni personalizzate, ad esempio un logger di console, un Registratore web o un Registratore di cronologia della console.

TVSDK genera messaggi di registro per molte delle sue attività, che il `PTLogFactory` inoltra a tutti i logger registrati. L’applicazione può inoltre generare messaggi di log personalizzati, che vengono inoltrati a tutti i logger registrati. Ogni logger può filtrare i messaggi e intraprendere le azioni appropriate.

Sono disponibili due implementazioni per `PTLogFactory`:

* Per ascoltare i log.
* Per aggiungere i registri a un `PTLogFactory`.

## Ascolta i registri {#listen-to-logs}

Per registrarsi per l&#39;ascolto dei log:
1. Implementa una classe personalizzata che segue il protocollo `PTLogger`:

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

1. Per registrare l&#39;istanza per ricevere le voci di log, aggiungi un&#39;istanza del `PTLogger` al `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

Ecco un esempio di filtraggio dei registri utilizzando il tipo `PTLogEntry` :

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

## Aggiungi nuovi messaggi di log {#add-new-log-messages}

Per registrarsi per ascoltare i log:
1. Crea un nuovo `PTLogEntry` e aggiungilo a `thePTLogFactory`:

   È possibile creare manualmente un&#39;istanza `PTLogEntry` e aggiungerla all&#39;istanza condivisa `PTLogFactory` oppure utilizzare una delle macro per eseguire la stessa operazione.

   Ecco un esempio di registrazione utilizzando la macro `PTLogDebug`:

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
