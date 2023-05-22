---
title: Inizializzare e configurare l’analisi video
description: Inizializzare e configurare l’analisi video
copied-description: true
exl-id: 26bdc11e-b8f6-414f-a3e9-53bc895d25ce
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Inizializzare e configurare l’analisi video {#initialize-and-configure-video-analytics}

Puoi configurare il lettore per il tracciamento e l’analisi dell’utilizzo dei video.
Prima di attivare il tracciamento video (heartbeat video), assicurati di disporre dei seguenti elementi:

* TVSDK 3.0 per Android.
* Informazioni su configurazione/inizializzazione

   Contatta il rappresentante di Adobe per informazioni specifiche sull’account di tracciamento video:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>Importante: il nome del file di configurazione JSON deve rimanere <span class="filepath"> ADBMobileConfig.json </span>. Impossibile modificare il nome e il percorso del file di configurazione. Il percorso di questo file deve essere <span class="filepath"> &lt;source root=""&gt;/assets </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Endpoint del server di tracciamento AppMeasurement </td> 
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


   1. Confermare che `ADBMobileConfig.json` Il file contiene i valori appropriati (forniti dall&#39;Adobe).
   1. Conferma che il file si trovi in `assets/` cartella.

      Questa cartella deve trovarsi nella radice della struttura di origine dell&#39;applicazione.

   1. Compila e genera l’applicazione.
   1. Distribuire ed eseguire l&#39;applicazione in bundle.

      Per ulteriori informazioni su queste impostazioni AppMeasurement, vedi [Misurazione dei video in Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en).

1. Inizializza e configura i metadati di tracciamento heartbeat video.

   >[!IMPORTANT]
   >
   >Puoi arrestare il modulo di analisi video nel flusso intermedio e reinizializzarlo, se necessario. Prima di reinizializzare il modulo, accertati che anche i metadati di analisi video siano aggiornati ai metadati di contenuto corretti. Per ricreare i metadati, ripeti i primi due passaggi seguenti (passaggi secondari) **a** e **b**).

   1. Crea un’istanza dei metadati di Video Analytics.

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

   1. Inizializza il provider Video Analytics.

      Dopo aver creato un’istanza del lettore multimediale, devi creare un’istanza del provider Video Analytics e fornirle il contesto dell’applicazione.

      >[!TIP]
      >
      >Crea sempre una nuova istanza del provider per ogni sessione di riproduzione dei contenuti e rimuovi il riferimento precedente dopo aver scollegato l’istanza del lettore multimediale.

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider = new VideoAnalyticsProvider(appContext); 
      ```

   1. Imposta i metadati di Video Analytics su `videoAnalyticsProvider` dell&#39;istanza.

      ```java
      videoAnalyticsProvider.setVideoAnalyticsMetadata(vaMetadata);
      ```

   1. Allega l’istanza del lettore multimediale a `videoAnalyticsProvider` istanza:

      ```java
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. Elimina il provider Video Analytics.

      Prima di iniziare una nuova sessione di riproduzione dei contenuti, elimina l’istanza precedente del provider video. Dopo aver ricevuto l’evento di completamento del contenuto (o la notifica), attendi alcuni minuti prima di eliminare l’istanza del provider di analisi video. Distruggere immediatamente l’istanza potrebbe interferire con la capacità del provider Video Analytics di inviare un ping &quot;video completato&quot;.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.detachMediaPlayer(); 
          videoAnalyticsProvider = null; 
      }
      ```

   1. Contrassegna manualmente il flusso live/lineare come completato.

      Se hai diversi episodi su un flusso live, puoi contrassegnare manualmente un episodio come completo utilizzando l’API completa. In questo modo si termina la sessione di tracciamento video per l’episodio video corrente e si può avviare una nuova sessione di tracciamento per l’episodio successivo.

      >[!TIP]
      >
      >Questa API è facoltativa e non funziona per il tracciamento video VOD.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.trackVideoComplete();    
      }
      ```
