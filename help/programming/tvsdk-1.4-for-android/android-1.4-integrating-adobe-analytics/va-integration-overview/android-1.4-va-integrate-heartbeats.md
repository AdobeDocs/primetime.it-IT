---
description: È possibile configurare il lettore per tenere traccia e analizzare l’utilizzo del video.
seo-description: È possibile configurare il lettore per tenere traccia e analizzare l’utilizzo del video.
seo-title: Inizializzare e configurare l'analisi video
title: Inizializzare e configurare l'analisi video
uuid: 262b1a28-2986-4fbb-a465-4ce8cefe18fb
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Inizializzare e configurare l&#39;analisi video{#initialize-and-configure-video-analytics}

È possibile configurare il lettore per tenere traccia e analizzare l’utilizzo del video.

Prima di attivare il tracciamento video (heartbeat video), accertatevi di disporre dei seguenti elementi:

* TVSDK per Android
* Informazioni su configurazione/inizializzazione - Contattate il rappresentante Adobe per ottenere informazioni specifiche sull’account di tracciamento video:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>Importante:  Il nome del file di configurazione JSON deve restare <span class="codeph"> ADBMobileConfig.json </span>. Impossibile modificare il nome e il percorso di questo file di configurazione. Il percorso di questo file deve essere <span class="codeph"> &lt;source root&gt;/assets </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Endpoint del server di tracciamento AppMeasurement </td> 
   <td colname="col2"> L'URL dell'endpoint della raccolta back-end di Adobe Analytics (ex SiteCatalyst). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Endpoint del server di tracciamento analisi video </td> 
   <td colname="col2"> URL dell'endpoint della raccolta back-end di analisi video. Qui vengono inviate tutte le chiamate di tracciamento heartbeat video. <p>Suggerimento:  L’URL del server di tracciamento dei visitatori è lo stesso dell’URL del server di tracciamento delle analisi. Per informazioni sull’implementazione del servizio ID visitatori, consulta <a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external"> Implementazione del servizio ID </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Nome account </td> 
   <td colname="col2"> Noto anche come ID Suite di rapporti (RSID). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ID organizzazione Marketing Cloud </td> 
   <td colname="col2"> Un valore stringa richiesto per creare un'istanza del componente Visitatore. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Editore </td> 
   <td colname="col2"> Si tratta dell'ID editore, fornito ai clienti dal loro rappresentante Adobe. <p>Suggerimento:  Questo ID non è solo una stringa con il nome del marchio o del televisore. </p> </td> 
  </tr> 
 </tbody> 
</table>

Per configurare il tracciamento video nel lettore:

1. Verificate che le opzioni di caricamento nel file della `ADBMobileConfig.json` risorsa siano corrette.

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

   Questo file di configurazione JSON viene fornito come risorsa con TVSDK. Il lettore legge questi valori solo al momento del caricamento e i valori rimangono costanti durante l&#39;esecuzione dell&#39;applicazione.

   Per configurare le opzioni di caricamento:

   1. Verificate che il `ADBMobileConfig.json` file contenga i valori appropriati forniti da Adobe.
   1. Verificate che il file si trovi nella `assets` cartella.

      Questa cartella deve trovarsi nella radice della struttura di origine dell&#39;applicazione.
   1. Compilate e create l&#39;applicazione.
   1. Implementare ed eseguire l&#39;applicazione fornita in bundle.

      Per ulteriori informazioni su queste impostazioni AppMeasurement, vedi [Misurazione dei video in Adobe Analytics](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/).
1. Inizializzare e configurare i metadati di tracciamento heartbeat video.

   >[!IMPORTANT]
   >
   >Potete arrestare il flusso midstream del modulo di analisi video e reinizializzarlo secondo necessità. Prima che il modulo venga reinizializzato, accertatevi che anche i metadati di analisi video vengano aggiornati ai metadati di contenuto corretti. Per ricreare i metadati, ripetete i passaggi secondari 1 e 2.

   1. Create un’istanza dei metadati di analisi video.

      Questa istanza contiene tutte le informazioni di configurazione necessarie per abilitare il tracciamento heartbeat video. Ad esempio:

      ```java
      private VideoAnalyticsMetadata getVideoAnalyticsTrackingMetadata() { 
          VideoAnalyticsMetadata vaMetadata = new VideoAnalyticsMetadata(); 
      
          vaMetadata.setTrackingServer("example.com"); 
          vaMetadata.setPublisher("sample-publisher"); 
          vaMetadata.setChannel("test-channel"); 
          vaMetadata.setVideoName("myvideo"); 
          vaMetadata.setVideoId("myvideoid"); 
          vaMetadata.setPlayerName("PSDK Player"); 
          vaMetadata.setUseSSL(false); 
          vaMetadata.debugLogging = true; // Set to NO for production deployment. 
          vaMetadata.quietMode = false; // Set to NO for production deployment. 
          vaMetadata.setEnableChapterTracking(true); 
          // use this API to override the default asset length -1 for live streams 
          vaMetadata.setAssetDuration(SAMPLE_ASSET_DURATION); 
      
          return vaMetadata; 
      }
      ```

   1. Aggiungete i metadati Video Analytics all’istanza di metadati globale.

      Una volta pronti, impostate l’istanza di metadati globale sulla risorsa multimediale o sull’elemento del lettore multimediale:

      ```java
      ((MetadataNode)resourceMetadata).setNode( 
            DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY.getValue(), vaMetadata);
      ```

   1. Inizializzare il tracciatore di analisi video.

      Dopo aver creato un’istanza del lettore multimediale, dovete creare un’istanza del tracciatore di Video Analytics e fornire un riferimento all’istanza del lettore multimediale.

      >[!TIP]
      >
      >Create sempre una nuova istanza di tracciamento per ogni sessione di riproduzione del contenuto e rimuovete il riferimento precedente dopo aver scollegato l’istanza del lettore multimediale.

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider =  
        new VideoAnalyticsProvider(appContext); 
      
      // Attach the TVSDK media player instance 
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. Distruggete il tracciatore di analisi video.

      Prima di iniziare una nuova sessione di riproduzione del contenuto, eliminate l’istanza precedente del tracciatore video. Dopo aver ricevuto l’evento di completamento del contenuto (o notifica), attendete alcuni minuti prima di eliminare l’istanza di tracciamento video. La distruzione immediata dell’istanza potrebbe interferire con la capacità del tracciatore di Video Analytics di inviare un ping video completo.

      ```java
      if (_videoAnalyticsProvider) { 
          _videoAnalyticsProvider.detachMediaPlayer(); 
          _videoAnalyticsProvider = null; 
      }
      ```

   1. Contrassegna manualmente il flusso Live/Linear come completato.

      Se disponete di vari episodi in uno streaming live, potete contrassegnare manualmente un episodio come completo utilizzando l&#39;API complete. In questo modo viene terminata la sessione di tracciamento video per l’episodio video corrente e potete avviare una nuova sessione di tracciamento per l’episodio successivo.

      >[!TIP]
      >
      >Questa API è facoltativa e non è necessaria per il tracciamento video VOD.

      ```java
      if (_videoAnalyticsProvider) { 
         _videoAnalyticsProvider.trackVideoComplete();    
      }
      ```

