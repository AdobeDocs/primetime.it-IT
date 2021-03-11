---
description: Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate sulla riproduzione, il buffering e i dispositivi.
title: Qualità delle statistiche del servizio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---


# Statistiche sulla qualità del servizio{#quality-of-service-statistics}

Quality of Service (QoS) offre una visualizzazione dettagliata delle prestazioni del motore video. TVSDK fornisce statistiche dettagliate sulla riproduzione, il buffering e i dispositivi.

## Leggi le statistiche relative a riproduzione, buffering e dispositivo QOS {#section_9996406E2D814FA382B77E3041CB02BC}

È possibile leggere le statistiche di riproduzione, buffering e dispositivo dalla classe `PTQOSProvider` .

La classe `PTQOSProvider` fornisce diverse statistiche, tra cui buffering, bit rate, frame rate, dati temporali e così via.

Fornisce inoltre informazioni sul dispositivo, ad esempio il modello, il sistema operativo e l’ID dispositivo del produttore.

>[!TIP]
>
>Non è possibile modificare la dimensione del buffer di riproduzione, ma è possibile monitorare lo stato della dimensione del buffer per il debug o l&#39;analisi. `PTPlaybackInformation` include proprietà quali  `playbackBufferFull` e  `playbackLikelyToKeepUp`.

1. Creare un&#39;istanza di un lettore multimediale.
1. Crea un oggetto `PTQOSProvider` e allegalo al lettore multimediale.

   Il costruttore `PTQOSProvider` prende il contesto di un lettore in modo che possa recuperare informazioni specifiche per il dispositivo.

   ```
   qosProvider = [[PTQOSProvider alloc]initWithPlayer:self.player]; 
   ```

1. (Facoltativo) Leggere le statistiche di riproduzione.

   Una soluzione per leggere le statistiche di riproduzione è quella di avere un timer, ad esempio un `NSTimer`, che recupera periodicamente i nuovi valori QoS dal `PTQOSProvider`. Ad esempio:

   ```
   - (void)printPlaybackInfoLog { 
       PTPlaybackInformation *playbackInfo = qosProvider.playbackInformation;  
       if (playbackInfo) { 
           // For example: 
           NSString *infoLog = [NSString stringWithFormat:@"observedBitrate :  
                                  %f\n",playbackInfo.observedBitrate]; 
           [consoleView logMessage:@"====%@\n\n",infoLog]; 
       } 
   }
   ```

1. (Facoltativo) Leggi le informazioni specifiche del dispositivo.

   ```
    PTDeviceInformation *devInfo = qosProvider.deviceInformation; 
   if (devInfo) { 
       [consoleView logMessage:@"=== qosDeviceInfo:==\n os =%@\n model =  
          %@\n id =%@\n\n", devInfo.os, devInfo.model, devInfo.id]; 
   } 
   [NSTimer scheduledTimerWithTimeInterval:2.0 target:self  
      selector:@selector(printPlaybackInfoLog) userInfo:nil repeats:YES];
   ```

