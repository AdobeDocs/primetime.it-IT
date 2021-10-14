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

Puoi configurare il lettore per tenere traccia e analizzare l’utilizzo dei video.
Prima di attivare il tracciamento video (heartbeat video), assicurati di disporre dei seguenti elementi:

* TVSDK 3.0 per Android.
* Informazioni di configurazione/inizializzazione

   Contatta il tuo rappresentante di Adobe per ottenere informazioni specifiche sul tuo account di tracciamento video:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json  </span> </td> 
   <td colname="col2"> <p>Importante:  Il nome del file di configurazione JSON deve rimanere <span class="filepath"> ADBMobileConfig.json </span>. Impossibile modificare il nome e il percorso del file di configurazione. Il percorso di questo file deve essere <span class="filepath"> &lt;source root&gt;/assets </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Endpoint server di tracciamento AppMeasurement </td> 
   <td colname="col2"> URL dell'endpoint di raccolta back-end Adobe Analytics (precedentemente SiteCatalyst). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Endpoint server di tracciamento analisi video </td> 
   <td colname="col2"> URL dell’endpoint di raccolta back-end di analisi video. Qui vengono inviate tutte le chiamate di tracciamento heartbeat video. <p>Suggerimento:  L’URL del server di tracciamento dei visitatori è lo stesso dell’URL del server di tracciamento di Analytics. Per informazioni sull’implementazione del servizio ID visitatori, consulta <a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external"> Implementare il servizio ID </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Nome account </td> 
   <td colname="col2"> Noto anche come ID della suite di rapporti (RSID). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ID organizzazione Marketing Cloud </td> 
   <td colname="col2"> Valore stringa necessario per creare un'istanza del componente Visitatore. </td> 
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


   1. Verifica che il file `ADBMobileConfig.json` contenga i valori appropriati (forniti dall’Adobe).
   1. Conferma che il file si trovi nella cartella `assets/` .

      Questa cartella deve trovarsi nella directory principale della struttura di origine dell&#39;applicazione.

   1. Compilare e creare l&#39;applicazione.
   1. Distribuisci ed esegui l&#39;applicazione in bundle.

      Per ulteriori informazioni su queste impostazioni di AppMeasurement, consulta [Misurazione di video in Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en).

1. Inizializzare e configurare i metadati di tracciamento heartbeat video.

   >[!IMPORTANT]
   >
   >È possibile arrestare il flusso midstream del modulo di analisi video e reinizializzarlo in base alle esigenze. Prima di reinizializzare il modulo, assicurati che i metadati di analisi video siano aggiornati anche ai metadati del contenuto corretti. Per ricreare i metadati, ripeti i primi due passaggi seguenti (passaggi secondari **a** e **b**).

   1. Crea un&#39;istanza dei metadati di Video Analytics.

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

   1. Inizializzare il provider di Video Analytics.

      Dopo aver creato un&#39;istanza del lettore multimediale, devi creare un&#39;istanza del provider Video Analytics e fornirgli il contesto dell&#39;applicazione.

      >[!TIP]
      >
      >Crea sempre una nuova istanza del provider per ogni sessione di riproduzione dei contenuti e rimuovi il riferimento precedente dopo aver scollegato l&#39;istanza del lettore multimediale.

      ```java
      VideoAnalyticsProvider videoAnalyticsProvider = new VideoAnalyticsProvider(appContext); 
      ```

   1. Imposta i metadati di Video Analytics sull&#39;istanza `videoAnalyticsProvider`.

      ```java
      videoAnalyticsProvider.setVideoAnalyticsMetadata(vaMetadata);
      ```

   1. Allega l&#39;istanza del lettore multimediale all&#39;istanza `videoAnalyticsProvider`:

      ```java
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. Distruggi il provider di Video Analytics.

      Prima di iniziare una nuova sessione di riproduzione dei contenuti, elimina l’istanza precedente del provider video. Dopo aver ricevuto l’evento di completamento del contenuto (o notifica), attendi alcuni minuti prima di eliminare l’istanza del provider di video analytics. La distruzione immediata dell’istanza potrebbe interferire con la capacità del provider di Video Analytics di inviare un ping &quot;video complete&quot;.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.detachMediaPlayer(); 
          videoAnalyticsProvider = null; 
      }
      ```

   1. Contrassegna manualmente il flusso Live/Lineare come completato.

      Se hai vari episodi su uno streaming live, puoi contrassegnare manualmente un episodio come completo utilizzando l&#39;API completa. Questo termina la sessione di tracciamento video per l&#39;episodio video corrente e puoi avviare una nuova sessione di tracciamento per l&#39;episodio successivo.

      >[!TIP]
      >
      >Questa API è opzionale e non funziona per il tracciamento video VOD.

      ```java
      if (videoAnalyticsProvider) { 
          videoAnalyticsProvider.trackVideoComplete();    
      }
      ```
