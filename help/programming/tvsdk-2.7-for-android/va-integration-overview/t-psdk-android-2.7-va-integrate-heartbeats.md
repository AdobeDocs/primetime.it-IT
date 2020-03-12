---
description: 'null'
seo-description: 'null'
seo-title: Inizializzare e configurare l'analisi video
title: Inizializzare e configurare l'analisi video
uuid: 98017a20-4997-42f7-9b03-fd9c4b6ccd92
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Inizializzare e configurare l&#39;analisi video {#initialize-and-configure-video-analytics}

È possibile configurare il lettore per tenere traccia e analizzare l’utilizzo del video.
Prima di attivare il tracciamento video (heartbeat video), accertatevi di disporre dei seguenti elementi:

* TVSDK 2.5 per Android.
* Informazioni di configurazione/inizializzazione

   Per informazioni specifiche sull’account di tracciamento video, contattate il vostro rappresentante Adobe:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>Importante:  Il nome del file di configurazione JSON deve restare <span class="filepath"> ADBMobileConfig.json </span>. Impossibile modificare il nome e il percorso di questo file di configurazione. Il percorso di questo file deve essere <span class="filepath"> &lt;source root&gt;/assets </span>. </p> </td> 
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
 </tbody> 
</table>

Per configurare il tracciamento video nel lettore:

1. Verificate che le opzioni di caricamento nel file della `ADBMobileConfig.json` risorsa siano corrette.

       &quot;
     {
     &quot;version&quot; : &quot;1.1&quot;,
     &quot;analytics&quot;: {
 &quot;     &quot;rsids&quot;: &quot;adobedevelopment&quot;,
     &quot;server&quot;: &quot;10.131.129.149:3000&quot;,
     &quot;charset&quot; : &quot;UTF-8&quot;,
     &quot;ssl&quot; : false,
     &quot;offlineEnabled&quot;: false,
     &quot;lifecycleTimeout&quot;: 5,
     &quot;batchLimit&quot; : 50,
     &quot;privacyDefault&quot; : &quot;optedin&quot;,
     &quot;poi&quot;: []
     },
     &quot;marketingCloud&quot;: {
 &quot;     org&quot;: &quot;VALORE FORNITO ADOBE&quot;
     },
     &quot;target&quot; : {
     &quot;clientCode&quot;: &quot;&quot;,
     &quot;timeout&quot;: 5
     },
     &quot;audienceManager&quot;: {
     &quot;server&quot;: &quot;&quot;
     }
     }
     &quot;
     
     Questo file di configurazione in formato JSON viene fornito come risorsa con TVSDK. Il lettore legge questi valori solo al momento del caricamento e i valori rimangono costanti durante l&#39;esecuzione dell&#39;applicazione.
       
 Per     configurare le opzioni relative al tempo di caricamento:
   
   1. Verificate che il `ADBMobileConfig.json` file contenga i valori appropriati (forniti da Adobe).
   1. Verificate che il file si trovi nella `assets/` cartella.

      Questa cartella deve trovarsi nella radice della struttura di origine dell&#39;applicazione.

   1. Compilate e create l&#39;applicazione.
   1. Implementare ed eseguire l&#39;applicazione fornita in bundle.

      Per ulteriori informazioni su queste impostazioni AppMeasurement, vedi [Misurazione dei video in Adobe Analytics](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/video/).

1. Inizializzare e configurare i metadati di tracciamento heartbeat video.

   >[!IMPORTANT]
   >
   >Potete arrestare il flusso midstream del modulo di analisi video e reinizializzarlo secondo necessità. Prima che il modulo venga reinizializzato, accertatevi che anche i metadati di analisi video vengano aggiornati ai metadati di contenuto corretti. Per ricreare i metadati, ripetete i primi due passaggi seguenti (passaggi secondari **a** e **b**).

   1. Create un’istanza dei metadati di analisi video.

      Questa istanza contiene tutte le informazioni di configurazione necessarie per abilitare il tracciamento heartbeat video. Ad esempio:

      ```java
      private VideoAnalyticsMetadata getVideoAnalyticsTrackingMetadata() { 
          VideoAnalyticsMetadata vaMetadata = new VideoAnalyticsMetadata(); 
      
          vaMetadata.setTrackingServer("example.com"); 
          vaMetadata.setChannel("test-channel"); 
          vaMetadata.setVideoName("myvideo"); 
          vaMetadata.setVideoId("myvideoid"); 
          vaMetadata.setPlayerName("PSDK Player"); 
          vaMetadata.setUseSSL(false); 
          vaMetadata.debugLogging = true; // Set to NO for production deployment. 
          vaMetadata.setEnableChapterTracking(true); 
          // use this API to override the default asset length -1 for live streams 
          vaMetadata.setAssetDuration(SAMPLE_ASSET_DURATION); 
      
          return vaMetadata; 
      }
      ```

   1. Inizializzare il fornitore di analisi video.

      Dopo aver creato un&#39;istanza del lettore multimediale, dovete creare un&#39;istanza del fornitore di Video Analytics e fornire il contesto dell&#39;applicazione a tale istanza.

      >[!TIP]
      >
      >Create sempre una nuova istanza del fornitore per ogni sessione di riproduzione del contenuto e rimuovete il riferimento precedente dopo aver scollegato l&#39;istanza del lettore multimediale.

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider = new VideoAnalyticsProvider(appContext); 
      ```

   1. Impostate i metadati Video Analytics sull’ `videoAnalyticsProvider` istanza.

      ```java
      videoAnalyticsProvider.setVideoAnalyticsMetadata(vaMetadata);
      ```

   1. Allegare l’istanza del lettore multimediale all’ `videoAnalyticsProvider` istanza:

      ```java
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. Distruggete il fornitore di analisi video.

      Prima di iniziare una nuova sessione di riproduzione del contenuto, eliminate l’istanza precedente del fornitore video. Dopo aver ricevuto l’evento di completamento del contenuto (o notifica), attendete alcuni minuti prima di distruggere l’istanza del fornitore di analisi video. La distruzione immediata dell’istanza potrebbe interferire con la capacità del fornitore di Analytics Video di inviare un ping &quot;video completato&quot;.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.detachMediaPlayer(); 
          videoAnalyticsProvider = null; 
      }
      ```

   1. Contrassegna manualmente il flusso Live/Linear come completato.

      Se disponete di vari episodi in uno streaming live, potete contrassegnare manualmente un episodio come completo utilizzando l&#39;API complete. In questo modo viene terminata la sessione di tracciamento video per l’episodio video corrente e potete avviare una nuova sessione di tracciamento per l’episodio successivo.

      >[!TIP]
      >
      >Questa API è opzionale e non funziona per il tracciamento video VOD.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.trackVideoComplete();    
      }
      ```

