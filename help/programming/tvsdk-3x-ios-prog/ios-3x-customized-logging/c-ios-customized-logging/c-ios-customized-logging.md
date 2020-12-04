---
description: Potete implementare un sistema di registrazione personalizzato.
seo-description: Potete implementare un sistema di registrazione personalizzato.
seo-title: Registrazione personalizzata
title: Registrazione personalizzata
uuid: f056d7d7-ec3a-4cf1-997f-72a89bbc9447
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---


# Registrazione personalizzata {#customized-logging}

Potete implementare un sistema di registrazione personalizzato.

Oltre a effettuare l’accesso utilizzando notifiche predefinite, puoi implementare un sistema di registrazione che utilizza i messaggi e i messaggi di registro generati da TVSDK. Per ulteriori informazioni sulle notifiche predefinite, vedere [Il sistema di notifica](https://help.adobe.com/en_US/primetime/psdk/ios/index.html#PSDKs-concept-The_Notification_System). È possibile utilizzare questi registri per risolvere i problemi delle applicazioni del lettore e per comprendere meglio il flusso di lavoro di riproduzione e pubblicità.

La registrazione personalizzata utilizza un&#39;istanza singleton condivisa di `PSDKPTLogFactory`, che fornisce un meccanismo per registrare i messaggi a più utenti di log. È possibile definire e aggiungere (registrare) uno o più logger al `PTLogFactory`. Questo consente di definire più logger con implementazioni personalizzate, ad esempio un console logger, un Web logger o un console History logger.

TVSDK genera messaggi di registro per molte delle sue attività, che vengono inoltrati da `PTLogFactory` a tutti i logger registrati. L&#39;applicazione può inoltre generare messaggi di registro personalizzati, che vengono inoltrati a tutti i logger registrati. Ogni logger può filtrare i messaggi e intervenire in modo appropriato.

Esistono due implementazioni per `PTLogFactory`:

* Per ascoltare i file di registro.
* Per aggiungere dei file di registro a `PTLogFactory`.

## Ascoltare i registri {#listen-to-logs}

Per registrarsi per ascoltare i file di registro:
1. Implementate una classe personalizzata che segue il protocollo `PTLogger`:

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

1. Per registrare l&#39;istanza per la ricezione delle voci di registrazione, aggiungere un&#39;istanza della `PTLogger` alla `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

Di seguito è riportato un esempio di filtraggio dei registri utilizzando il tipo `PTLogEntry`:

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

Per registrarsi per ascoltare i registri:

Create un nuovo `PTLogEntry` e aggiungetelo a `thePTLogFactory`:

È possibile creare manualmente un&#39;istanza `PTLogEntry` e aggiungerla all&#39;istanza condivisa `PTLogFactory` oppure utilizzare una delle macro per eseguire la stessa operazione.

Di seguito è riportato un esempio di registrazione utilizzando la macro `PTLogDebug`:

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
