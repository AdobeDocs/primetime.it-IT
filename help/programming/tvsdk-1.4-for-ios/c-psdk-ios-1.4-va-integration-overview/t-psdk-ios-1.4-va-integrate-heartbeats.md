---
description: Puoi configurare il lettore per tenere traccia e analizzare l’utilizzo dei video.
title: Inizializzare e configurare l’analisi video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---


# Inizializzare e configurare l&#39;analisi video{#initialize-and-configure-video-analytics}

Puoi configurare il lettore per tenere traccia e analizzare l’utilizzo dei video.

Prima di attivare il tracciamento video (heartbeat video), assicurati di disporre dei seguenti elementi:

* TVSDK per iOS
* Informazioni di configurazione/inizializzazione - Contatta il tuo rappresentante di Adobe per informazioni specifiche sul tuo account di tracciamento video:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json  </span> </td> 
   <td colname="col2"> <p>Importante:  Il nome del file di configurazione JSON deve rimanere <span class="codeph"> ADBMobileConfig.json </span>. Impossibile modificare il nome e il percorso del file di configurazione. Il percorso di questo file deve essere <span class="codeph"> &lt;source root&gt;/AdobeMobile </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Endpoint server  </span> di tracciamento AppMeasurement </td> 
   <td colname="col2"> URL dell'endpoint di raccolta back-end Adobe Analytics (precedentemente SiteCatalyst). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Endpoint server di tracciamento analisi video </td> 
   <td colname="col2"> URL dell’endpoint di raccolta back-end di analisi video. Qui vengono inviate tutte le chiamate di tracciamento heartbeat video. <p>Suggerimento:  L’URL del server di tracciamento dei visitatori è lo stesso dell’URL del server di tracciamento di Analytics. Per informazioni sull’implementazione del servizio ID visitatori, consulta <a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external"> Implementare il servizio ID </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Nome account </td> 
   <td colname="col2"> Noto anche come ID della suite di rapporti (RSID). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ID organizzazione Marketing Cloud </td> 
   <td colname="col2"> Valore stringa necessario per creare un'istanza del componente Visitatore. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Editore </td> 
   <td colname="col2"> Questo è l'ID editore, fornito ai clienti dal loro rappresentante Adobe. <p>Suggerimento:  Questo ID non è solo una stringa con il nome del brand/televisore. </p> </td> 
  </tr> 
 </tbody> 
</table>

Per configurare il tracciamento video nel lettore:

1. Conferma che le opzioni di caricamento nel file di risorse `ADBMobileConfig.json` siano corrette.

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

   Questo file di configurazione in formato JSON è incluso come risorsa con TVSDK. Il lettore legge questi valori solo al momento del caricamento e i valori rimangono costanti durante l&#39;esecuzione dell&#39;applicazione.

   Per configurare le opzioni di caricamento:

   1. Verifica che il file `ADBMobileConfig.json` contenga i valori appropriati forniti dall&#39;Adobe.
   1. Conferma che il file si trovi nella cartella `AdobeMobile` .

      Questa cartella deve trovarsi nella directory principale della struttura di origine dell&#39;applicazione.
   1. Compilare e creare l&#39;applicazione.
   1. Distribuisci ed esegui l&#39;applicazione in bundle.

      Per ulteriori informazioni su queste impostazioni di AppMeasurement, consulta [Misurazione di video in Adobe Analytics](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/).
1. Inizializzare e configurare i metadati di tracciamento heartbeat video.

   >[!IMPORTANT]
   >
   >È possibile arrestare il flusso midstream del modulo di analisi video e reinizializzarlo in base alle esigenze. Prima di reinizializzare il modulo, assicurati che i metadati di analisi video siano aggiornati anche ai metadati del contenuto corretti. Per ricreare i metadati, ripeti i passaggi secondari 1 e 2.

   1. Crea un&#39;istanza dei metadati di Video Analytics.

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

      Quando sei pronto, imposta l’istanza di metadati globale sulla risorsa multimediale o sull’elemento del lettore multimediale:

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

   1. Inizializzare il tracker di Video Analytics.

      Dopo aver creato un&#39;istanza di lettore multimediale, devi creare un&#39;istanza di tracciamento di Video Analytics e fornire un riferimento all&#39;istanza di lettore multimediale.

      >[!TIP]
      >
      >Crea sempre una nuova istanza tracker per ogni sessione di riproduzione dei contenuti e rimuovi il riferimento precedente dopo aver scollegato l&#39;istanza del lettore multimediale.

      ```
      self.videoAnalyticsTracker =  
        [[[PTVideoAnalyticsTracker alloc] initWithMediaPlayer:self.player] autorelease];
      ```

   1. Distruggi il tracker di Video Analytics.

      Prima di iniziare una nuova sessione di riproduzione dei contenuti, elimina l’istanza precedente del tracker di video. Dopo aver ricevuto l’evento di completamento del contenuto (o notifica), attendi alcuni minuti prima di eliminare l’istanza di tracciamento video. La distruzione immediata dell’istanza potrebbe interferire con la capacità del tracker di Video Analytics di inviare un ping completo del video.

      ```
      self.videoAnalyticsTracker = nil;
      ```

   1. Contrassegna manualmente il flusso Live/Lineare come completato.

      Se hai vari episodi su uno streaming live, puoi contrassegnare manualmente un episodio come completo utilizzando l&#39;API completa. Questo termina la sessione di tracciamento video per l&#39;episodio video corrente e puoi avviare una nuova sessione di tracciamento per l&#39;episodio successivo.

      >[!TIP]
      >
      >Questa API è facoltativa e non è necessaria per il tracciamento video VOD.

      ```
      if (self.videoAnalyticsTracker) 
      { 
         [self.videoAnalyticsTracker trackVideoComplete];   
      }
      ```

