---
description: Puoi configurare il lettore per il tracciamento e l’analisi dell’utilizzo dei video.
title: Inizializzare e configurare l’analisi video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---

# Inizializzare e configurare l’analisi video{#initialize-and-configure-video-analytics}

Puoi configurare il lettore per il tracciamento e l’analisi dell’utilizzo dei video.

Prima di attivare il tracciamento video (heartbeat video), assicurati di disporre dei seguenti elementi:

* TVSDK per HLS desktop
* Informazioni su configurazione/inizializzazione - Contatta il rappresentante di Adobe per informazioni specifiche sull’account di tracciamento video:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
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
  <tr> 
   <td colname="col1"> Endpoint del server di tracciamento dei visitatori </td> 
   <td colname="col2"> L’URL dell’endpoint back-end che fornisce un identificatore univoco per il visualizzatore video corrente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Editore </td> 
   <td colname="col2"> Questo è l’ID dell’editore, fornito ai clienti dal loro rappresentante Adobe. <p>Suggerimento: questo ID non è solo una stringa con il nome del brand/televisore. </p> </td> 
  </tr> 
 </tbody> 
</table>

Per configurare il tracciamento video nel lettore:

1. Crea un’istanza e configura la libreria VisitorAPI.

       Considera le seguenti informazioni:
   
   * La creazione di un&#39;istanza richiede un parametro di input dell&#39;ID organizzazione del Marketing Cloud fornito da Adobe.

     Questo è un valore stringa.
   * L’unica opzione di configurazione per la libreria VisitorAPI è l’URL dell’endpoint back-end che fornisce l’identificatore univoco per l’utente corrente.
   * L’URL del server di tracciamento dei visitatori è uguale all’URL del server di tracciamento di Analytics.

     Per informazioni sull’implementazione del servizio ID visitatori, consulta Implementazione del servizio ID visitatori.

   ```
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID"); 
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”; 
   ```

1. Crea un’istanza e configura il componente AppMeasurement.

   L’istanza di AppMeasurement dispone di molte opzioni di configurazione. Per ulteriori informazioni, vedere [Sviluppatore Adobe Analytics](https://microsite.omniture.com/t2/help/en_US/reference/#Developer) documentazione. Le opzioni nel codice di esempio seguente ( `account`, `visitorNamespace`, e `trackingServer`) e i valori sono forniti da Adobe.

   >[!IMPORTANT]
   >
   >È necessario assicurarsi che la catena di dipendenze sia impostata correttamente. L’istanza di AppMeasurement aggrega (dipende da) il componente API visitatore.

   ```
   // Instantiate and configure AppMeasurement 
   
   // Instantiate AppMeasurement instance only once! 
   if (_appMeasurementObject == null) {  
       _appMeasurementObject = new AppMeasurement(); 
   } 
   
   with (_appMeasurementObject) { 
       account = "ACCOUNT_NAME"; // Also known as RSID 
       trackingServer = "URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER"; 
   
       // Use the same value here as for the Visitor API component 
       visitorNamespace = "MARKETING_CLOUD_ORG_ID"; 
   
       // Attach the Visitor API to the AppMeasurement instance. 
       visitor = _visitor;  
       pageName = "pageName"; 
       charSet = "UTF-8"; 
       currencyCode = "USD"; 
   } 
   ```

   >[!IMPORTANT]
   >
   >Nell’applicazione, assicurati che `appMeasurementObject.visitor` viene popolato prima di avviare il flusso di analisi video, oppure potresti non ottenere alcun risultato di tracciamento. Questi risultati sono indicati dai messaggi nel registro. Puoi aggiungere una chiamata di tracciamento vuota ( `appMeasurementObject.track`), polling `visitor` finché non viene popolato, quindi avvia video analytics.

1. Inizializza e configura i metadati di tracciamento heartbeat video.

   >[!IMPORTANT]
   >
   >Puoi arrestare il modulo di analisi video nel flusso intermedio e reinizializzarlo, se necessario. Prima di reinizializzare il modulo, accertati che anche i metadati di analisi video siano aggiornati ai metadati di contenuto corretti. Per ricreare i metadati, ripeti i passaggi secondari 1 e 2.

   1. Crea un’istanza dei metadati di Video Analytics.

      Questa istanza contiene tutte le informazioni di configurazione necessarie per abilitare il tracciamento heartbeat video. Ad esempio:

      ```
      private function getVideoAnalyticsTrackingMetadata():VideoAnalyticsMetadata {     
          // Initialize visitor id service and appMeasurement      
          [...] // as shown in the previous steps     
      
          var vaMetadata:VideoAnalyticsMetadata = new VideoAnalyticsMetadata(); 
      
          with (vaMetadata) { 
              trackingServer = "hbTrackingServer"; 
              publisher = "hbPublisher"; 
              channel = "hbChannel";  
              playerName = "hbPlayerName"; 
      
              // this overwrites the ContextData variable a.media.friendlyName 
              videoName = "hbFriendlyName";  
      
              // this will overwrite the ContextData variable a.media.name 
              videoId = "hbName"; 
      
              enableChapterTracking = true; 
      
              // Set these to false for production deployment 
              debugLogging = true;  
              quietMode = false; 
      
          } 
      } 
      ```

   1. Aggiungi i metadati di Video Analytics all’istanza di metadati globale.

      Quando sei pronto, imposta l’istanza dei metadati globali sulla risorsa multimediale o sull’elemento del lettore multimediale:

      ```
      var resourceMetadata:Metadata = _player.currentItem.resource.metadata; 
      resourceMetadata.setMetadata(DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY,  
                                   getVideoAnalyticsTrackingMetadata());
      ```

   1. Inizializza il tracker di Video Analytics.

      Dopo aver creato un’istanza del lettore multimediale, devi creare un’istanza di tracciamento di Video Analytics e fornire un riferimento a tale istanza.

      >[!TIP]
      >
      >Crea sempre una nuova istanza di tracciamento per ogni sessione di riproduzione del contenuto e rimuovi il riferimento precedente dopo aver scollegato l’istanza del lettore multimediale.

      ```
      _videoAnalyticsProvider = new VideoAnalyticsProvider(_appMeasurementObject); 
      _videoAnalyticsProvider.attachMediaPlayer(_player);
      ```

   1. Distruggi il tracker di Video Analytics.

      Prima di iniziare una nuova sessione di riproduzione del contenuto, elimina l’istanza precedente del tracciatore video. Dopo aver ricevuto l’evento di completamento del contenuto (o la notifica), attendi alcuni minuti prima di eliminare l’istanza di tracciamento video. Distruggere immediatamente l’istanza potrebbe interferire con la capacità del tracciatore di Video Analytics di inviare un ping video completo.

      ```
      if (videoAnalyticsTracker) { 
          videoAnalyticsTracker.detachMediaPlayer(); 
          videoAnalyticsTracker = null; 
      }
      ```

   1. Contrassegna manualmente il flusso live/lineare come completato.

      Se hai diversi episodi su un flusso live, puoi contrassegnare manualmente un episodio come completo utilizzando l’API completa. In questo modo si termina la sessione di tracciamento video per l’episodio video corrente e si può avviare una nuova sessione di tracciamento per l’episodio successivo.

      >[!TIP]
      >
      >Questa API è facoltativa e non è necessaria per il tracciamento video VOD.
