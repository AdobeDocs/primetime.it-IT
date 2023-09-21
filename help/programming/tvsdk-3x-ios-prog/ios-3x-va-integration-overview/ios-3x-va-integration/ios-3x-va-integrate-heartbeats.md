---
description: Puoi configurare il lettore per il tracciamento e l’analisi dell’utilizzo dei video.
title: Inizializzare e configurare l’analisi video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Inizializzare e configurare l’analisi video {#initialize-and-configure-video-analytics}

Puoi configurare il lettore per il tracciamento e l’analisi dell’utilizzo dei video.

Prima di attivare il tracciamento video (heartbeat video), assicurati di disporre dei seguenti elementi:

* TVSDK per iOS
* Informazioni su configurazione/inizializzazione - Contatta il rappresentante di Adobe per informazioni specifiche sull’account di tracciamento video:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>Importante: il nome del file di configurazione JSON deve rimanere <span class="codeph"> ADBMobileConfig.json </span>. Impossibile modificare il nome e il percorso del file di configurazione. Il percorso di questo file deve essere <span class="codeph"> &lt;source root=""&gt;/AdobeMobile </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AppMeasurement </span> endpoint del server di tracciamento </td> 
   <td colname="col2"> URL dell’endpoint di raccolta back-end Adobe Analytics (precedentemente SiteCatalyst). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Endpoint del server di tracciamento di Video Analytics </td> 
   <td colname="col2"> URL dell’endpoint della raccolta back-end di analisi video. Qui vengono inviate tutte le chiamate di tracciamento heartbeat video. <p>Suggerimento: l'URL del server di tracciamento dei visitatori corrisponde all'URL del server di tracciamento di Analytics. Per informazioni sull'implementazione del servizio ID visitatori, vedi <a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external"> Implementazione del servizio ID </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Nome account </td> 
   <td colname="col2"> Noto anche come ID suite di rapporti (RSID). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ID organizzazione Marketing Cloud </td> 
   <td colname="col2"> Valore stringa necessario per creare un’istanza del componente Visitatore. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Editore </td> 
   <td colname="col2"> Questo è l’ID dell’editore, fornito ai clienti dal loro rappresentante Adobe. <p>Suggerimento: questo ID non è solo una stringa con il nome del brand/televisore. </p> </td> 
  </tr> 
 </tbody> 
</table>

Per configurare il tracciamento video nel lettore:

1. Conferma che le opzioni di caricamento nel `ADBMobileConfig.json` il file di risorse è corretto.

   ```
   { 
       "version" : "1.1", 
       "analytics" : { 
           "rsids" : "adobedevelopment", 
           "server" : "10.131.129.149:3000", 
           "charset" : "UTF-8", 
           "ssl" : false, 
           "offlineEnabled" : false, 
           "lifecycleTimeout" : 5, 
           "batchLimit" : 50, 
           "privacyDefault" : "optedin", 
           "poi" : [] 
       }, 
       "marketingCloud": { 
           "org": "ADOBE PROVIDED VALUE"  
       }, 
       "target" : { 
           "clientCode" : "", 
           "timeout" : 5 
       }, 
       "audienceManager" : { 
           "server" : "" 
       } 
   }
   ```

   Questo file di configurazione in formato JSON è incluso come risorsa con TVSDK. Il lettore legge questi valori solo al momento del caricamento e i valori rimangono costanti durante l’esecuzione dell’applicazione.

   Per configurare le opzioni del tempo di caricamento:

   1. Confermare che `ADBMobileConfig.json` contiene i valori appropriati forniti da Adobe.
   1. Conferma che il file si trovi in `AdobeMobile` cartella.

      Questa cartella deve trovarsi nella radice della struttura di origine dell&#39;applicazione.
   1. Compila e genera l’applicazione.
   1. Distribuire ed eseguire l&#39;applicazione in bundle.

      Per ulteriori informazioni su queste impostazioni di AppMeasurement, vedi [Misurazione dei video in Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en).
1. Inizializza e configura i metadati di tracciamento heartbeat video.

   >[!IMPORTANT]
   >
   >Puoi arrestare il modulo di analisi video nel flusso intermedio e reinizializzarlo, se necessario. Prima di reinizializzare il modulo, accertati che anche i metadati di analisi video siano aggiornati ai metadati di contenuto corretti. Per ricreare i metadati, ripeti i passaggi secondari 1 e 2.

   1. Crea un’istanza dei metadati di Video Analytics.

      Questa istanza contiene tutte le informazioni di configurazione necessarie per abilitare il tracciamento heartbeat video. Ad esempio:

      ```
      - (PTVideoAnalyticsTrackingMetadata *)getVideoAnalyticsTrackingMetadata 
      { 
          PTVideoAnalyticsTrackingMetadata *vaTrackingMetadata =  
            [[[PTVideoAnalyticsTrackingMetadata alloc]  
                 initWithTrackingServer:@"example.com" 
                 publisher:@"sample-publisher"] autorelease]; 
      
          // Set these to NO for production deployment. 
          vaTrackingMetadata.debugLogging = YES;  
          vaTrackingMetadata.quietMode = NO; 
      
          vaTrackingMetadata.channel = @"test-channel"; 
          vaTrackingMetadata.videoName = @"myvideo"; 
          vaTrackingMetadata.videoId = @"myvideoid"; 
          vaTrackingMetadata.playerName = @"PSDK Player"; 
          vaTrackingMetadata.enableChapterTracking = YES; 
          vaTrackingMetadata.useSSL = NO; 
          // use this API to override the default asset length -1 for live streams 
          vaTrackingMetadata.assetDuration = SAMPLE_ASSET_DURATION; 
      
      }
      ```

   1. Aggiungi i metadati di Video Analytics all’istanza di metadati globale.

      Quando sei pronto, imposta l’istanza dei metadati globali sulla risorsa multimediale o sull’elemento del lettore multimediale:

      ```
      - (PTMetadata *)createMetadata 
      { 
          PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
      
          [metadata setMetadata:[self getVideoAnalyticsTrackingMetadata]  
            forKey:PTVideoAnalyticsTrackingMetadataKey]; 
      
          return metadata; 
      } 
      
      PTMetadata *metadata = [self createMetadata]; 
      
      PTMediaPlayerItem *item =  
        [[[PTMediaPlayerItem alloc] initWithUrl:[[[NSURL alloc]  
          initWithString:@"media-url"] autorelease] 
          mediaId:@"media-id" metadata:metadata] autorelease];
      ```

   1. Inizializza il tracker di Video Analytics.

      Dopo aver creato un’istanza del lettore multimediale, devi creare un’istanza di tracciamento di Video Analytics e fornire un riferimento a tale istanza.

      >[!TIP]
      >
      >Crea sempre una nuova istanza di tracciamento per ogni sessione di riproduzione del contenuto e rimuovi il riferimento precedente dopo aver scollegato l’istanza del lettore multimediale.

      ```
      self.videoAnalyticsTracker =  
        [[[PTVideoAnalyticsTracker alloc] initWithMediaPlayer:self.player] autorelease];
      ```

   1. Distruggi il tracker di Video Analytics.

      Prima di iniziare una nuova sessione di riproduzione del contenuto, elimina l’istanza precedente del tracciatore video. Dopo aver ricevuto l’evento di completamento del contenuto (o la notifica), attendi alcuni minuti prima di eliminare l’istanza di tracciamento video. Distruggere immediatamente l’istanza potrebbe interferire con la capacità del tracciatore di Video Analytics di inviare un ping video completo.

      ```
      self.videoAnalyticsTracker = nil;
      ```

   1. Contrassegna manualmente il flusso live/lineare come completato.

      Se hai diversi episodi su un flusso live, puoi contrassegnare manualmente un episodio come completo utilizzando l’API completa. In questo modo si termina la sessione di tracciamento video per l’episodio video corrente e si può avviare una nuova sessione di tracciamento per l’episodio successivo.

      >[!TIP]
      >
      >Questa API è facoltativa e non è necessaria per il tracciamento video VOD.

      ```
      if (self.videoAnalyticsTracker) 
      { 
         [self.videoAnalyticsTracker trackVideoComplete];   
      }
      ```
