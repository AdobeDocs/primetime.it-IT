---
description: È possibile configurare il lettore per tenere traccia e analizzare l’utilizzo del video.
seo-description: È possibile configurare il lettore per tenere traccia e analizzare l’utilizzo del video.
seo-title: Inizializzare e configurare l'analisi video
title: Inizializzare e configurare l'analisi video
uuid: ece5ddc1-3f7b-4878-b1bc-1fec0a459add
translation-type: tm+mt
source-git-commit: 6cb3463be8986d8a1dc718655bd929a0f07ac00d
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---


# Inizializzare e configurare l&#39;analisi video{#initialize-and-configure-video-analytics}

È possibile configurare il lettore per tenere traccia e analizzare l’utilizzo del video.

Prima di attivare il tracciamento video (heartbeat video), accertatevi di disporre dei seguenti elementi:

* TVSDK per desktop HLS
* Informazioni di configurazione/inizializzazione - Contattate il rappresentante del Adobe  per informazioni specifiche sull’account di tracciamento video:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> Endpoint del server di tracciamento AppMeasurement </td> 
   <td colname="col2"> L'URL dell'endpoint della raccolta back-end di Adobe Analytics  (precedentemente SiteCatalyst). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Endpoint del server di tracciamento analisi video </td> 
   <td colname="col2"> URL dell'endpoint della raccolta back-end di analisi video. Qui vengono inviate tutte le chiamate di tracciamento heartbeat video. <p>Suggerimento:  L’URL del server di tracciamento dei visitatori è lo stesso dell’URL del server di tracciamento delle analisi. Per informazioni sull'implementazione del servizio ID visitatori, vedi <a href="https://marketing.adobe.com/resources/help/en_US/mcvid/mcvid-setup-target.html" format="html" scope="external"> Implementare il servizio ID </a>. </p> </td> 
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
   <td colname="col1"> Endpoint del server di tracciamento visitatori </td> 
   <td colname="col2"> L’URL dell’endpoint back-end che fornisce un identificatore univoco per il visualizzatore video corrente. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Editore </td> 
   <td colname="col2"> Si tratta dell'ID editore, fornito ai clienti dal rappresentante del Adobe . <p>Suggerimento:  Questo ID non è solo una stringa con il nome del marchio o del televisore. </p> </td> 
  </tr> 
 </tbody> 
</table>

Per configurare il tracciamento video nel lettore:

1. Creare un&#39;istanza e configurare la libreria VisitorAPI.

       Tenete presenti le seguenti informazioni:
   
   * L&#39;istanza richiede un parametro di input ID organizzazione Marketing Cloud fornito da  Adobe.

      Si tratta di un valore di stringa.
   * L&#39;unica opzione di configurazione per la libreria VisitorAPI è l&#39;URL dell&#39;endpoint back-end che fornisce l&#39;identificatore univoco per l&#39;utente corrente.
   * L’URL del server di tracciamento dei visitatori è lo stesso dell’URL del server di tracciamento delle analisi.

      Per informazioni sull’implementazione del servizio ID visitatori, vedi Implementazione del servizio ID visitatori.

   ```
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID"); 
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”; 
   ```

1. Creare un&#39;istanza e configurare il componente AppMeasurement.

   L’istanza AppMeasurement presenta diverse opzioni di configurazione. Per ulteriori informazioni, consultare la [ documentazione Adobe Analytics Developer](https://microsite.omniture.com/t2/help/en_US/reference/#Developer). Le opzioni nel seguente codice di esempio ( `account`, `visitorNamespace` e `trackingServer`) sono obbligatorie e i valori sono forniti da  Adobe.

   >[!IMPORTANT]
   >
   >È necessario assicurarsi che la catena di dipendenze sia impostata correttamente. L’istanza AppMeasurement aggrega (dipende da) il componente API del visitatore.

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
   >Nell&#39;applicazione, assicurarsi che `appMeasurementObject.visitor` sia popolato prima di avviare il flusso di analisi video, oppure che non si ottengano risultati di tracciamento. Questi risultati sono indicati dai messaggi presenti nel registro. Potete aggiungere una chiamata di tracciamento vuota ( `appMeasurementObject.track`), eseguire il polling della proprietà `visitor` finché non viene compilata e avviare l&#39;analisi dei video.

1. Inizializzare e configurare i metadati di tracciamento heartbeat video.

   >[!IMPORTANT]
   >
   >Potete arrestare il flusso midstream del modulo di analisi video e reinizializzarlo secondo necessità. Prima che il modulo venga reinizializzato, accertatevi che anche i metadati di analisi video vengano aggiornati ai metadati di contenuto corretti. Per ricreare i metadati, ripetete i passaggi secondari 1 e 2.

   1. Create un’istanza dei metadati di analisi video.

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

   1. Aggiungete i metadati Video Analytics all’istanza di metadati globale.

      Una volta pronti, impostate l’istanza di metadati globale sulla risorsa multimediale o sull’elemento del lettore multimediale:

      ```
      var resourceMetadata:Metadata = _player.currentItem.resource.metadata; 
      resourceMetadata.setMetadata(DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY,  
                                   getVideoAnalyticsTrackingMetadata());
      ```

   1. Inizializzare il tracciatore di analisi video.

      Dopo aver creato un’istanza del lettore multimediale, dovete creare un’istanza del tracciatore di Video Analytics e fornire un riferimento all’istanza del lettore multimediale.

      >[!TIP]
      >
      >Create sempre una nuova istanza di tracciamento per ogni sessione di riproduzione del contenuto e rimuovete il riferimento precedente dopo aver scollegato l’istanza del lettore multimediale.

      ```
      _videoAnalyticsProvider = new VideoAnalyticsProvider(_appMeasurementObject); 
      _videoAnalyticsProvider.attachMediaPlayer(_player);
      ```

   1. Distruggete il tracciatore di analisi video.

      Prima di iniziare una nuova sessione di riproduzione del contenuto, eliminate l’istanza precedente del tracciatore video. Dopo aver ricevuto l’evento di completamento del contenuto (o notifica), attendete alcuni minuti prima di eliminare l’istanza di tracciamento video. La distruzione immediata dell’istanza potrebbe interferire con la capacità del tracciatore di Video Analytics di inviare un ping video completo.

      ```
      if (videoAnalyticsTracker) { 
          videoAnalyticsTracker.detachMediaPlayer(); 
          videoAnalyticsTracker = null; 
      }
      ```

   1. Contrassegna manualmente il flusso Live/Linear come completato.

      Se disponete di vari episodi in uno streaming live, potete contrassegnare manualmente un episodio come completo utilizzando l&#39;API complete. In questo modo viene terminata la sessione di tracciamento video per l’episodio video corrente e potete avviare una nuova sessione di tracciamento per l’episodio successivo.

      >[!TIP]
      >
      >Questa API è facoltativa e non è necessaria per il tracciamento video VOD.

