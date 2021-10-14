---
description: Puoi configurare il lettore per tenere traccia e analizzare l’utilizzo dei video.
title: Inizializzare e configurare l’analisi video
exl-id: e0bf461b-a431-4fba-bd3d-c38be307a92f
source-git-commit: 3bbf70e07b51585c9b53f470180d55aa7ac084bc
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Inizializzare e configurare l’analisi video {#initialize-and-configure-video-analytics}

Puoi configurare il lettore per tenere traccia e analizzare l’utilizzo dei video.

Prima di attivare il tracciamento video (heartbeat video), assicurati di disporre dei seguenti elementi:

* Informazioni di inizializzazione TVSDK Configurazione/Browser - Contatta il tuo rappresentante di Adobe per informazioni specifiche sul tuo account di tracciamento video:

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84">
 <tbody>
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
  <tr>
   <td colname="col1"> Endpoint server di tracciamento visitatori </td>
   <td colname="col2"> URL dell’endpoint back-end che fornisce un identificatore univoco per il visualizzatore video corrente. </td>
  </tr>
  <tr>
   <td colname="col1"> Editore </td>
   <td colname="col2"> Questo è l'ID editore, fornito ai clienti dal loro rappresentante Adobe. <p>Suggerimento:  Questo ID non è solo una stringa con il nome del brand/televisore. </p> </td>
  </tr>
 </tbody>
</table>

Per configurare il tracciamento video nel lettore:

1. Crea un&#39;istanza e configura la libreria VisitorAPI.

       Considera le seguenti informazioni:
   
   * La creazione di un&#39;istanza richiede un parametro di input dell&#39;ID organizzazione Marketing Cloud fornito da Adobe.

      Questo è un valore stringa.
   * L&#39;unica opzione di configurazione per la libreria VisitorAPI è l&#39;URL dell&#39;endpoint di back-end che fornisce l&#39;identificatore univoco per l&#39;utente corrente.
   * L’URL del server di tracciamento dei visitatori è lo stesso dell’URL del server di tracciamento di Analytics.

      Per informazioni sull&#39;implementazione del servizio ID visitatori, consulta [Implementazione del servizio ID visitatori](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en).

   ```js
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID");
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”;
   ```

2. Crea un&#39;istanza e configura il componente AppMeasurement.

   L&#39;istanza AppMeasurement dispone di molte opzioni di configurazione. Per ulteriori informazioni, consulta la documentazione [Adobe Analytics Developer](https://microsite.omniture.com/t2/help/en_US/reference/#Developer) . Le opzioni nel seguente codice di esempio ( `account`, `visitorNamespace` e `trackingServer`) sono obbligatorie e i valori sono forniti da un Adobe.

   >[!IMPORTANT]
   >
   >È necessario assicurarsi che la catena di dipendenze sia impostata correttamente. L’istanza AppMeasurement aggrega (dipende da) il componente API del visitatore.

   ```js
   var appMeasurement = new AppMeasurement();
   appMeasurement.visitor = visitor;
   appMeasurement.trackingServer = 'URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER';
   appMeasurement.account = 'ACCOUNT_NAME'; // Also known as RSID
   appMeasurement.pageName = 'Sample Page Name';
   appMeasurement.charSet = "UTF-8";
   appMeasurement.visitorID = "test-vid";
   ```

   >[!IMPORTANT]
   >
   >Nell’applicazione, assicurati che `appMeasurementObject.visitor` sia popolato prima di avviare il flusso di analisi video, altrimenti potresti non ottenere alcun risultato di tracciamento. Questi risultati sono indicati dai messaggi nel registro. Puoi aggiungere una chiamata di tracciamento vuota ( `appMeasurementObject.track`), eseguire il polling della proprietà `visitor` fino a quando non viene compilata e avviare l&#39;analisi video.

3. Inizializzare e configurare i metadati di tracciamento heartbeat video.

   >[!IMPORTANT]
   >
   >È possibile arrestare il flusso midstream del modulo di analisi video e reinizializzarlo in base alle esigenze. Prima di reinizializzare il modulo, assicurati che i metadati di analisi video siano aggiornati anche ai metadati del contenuto corretti. Per ricreare i metadati, ripeti i passaggi secondari 1 e 2.

   1. Crea un&#39;istanza dei metadati di Video Analytics.
Questa istanza contiene tutte le informazioni di configurazione necessarie per abilitare il tracciamento heartbeat video. Ad esempio:

      ```js
      function getVideoAnalyticsMetadata() {
          var vaObj = new AdobePSDK.VA.VideoAnalyticsMetadata();
          vaObj.appMeasurement = appMeasurement;
          vaObj.trackingServer = 'hbTrackingServer';
          vaObj.publisher = 'hbPublisher';
          vaObj.channel = 'sample-channel';
          vaObj.playerName = 'TVSDK-HTML';
          vaObj.appVersion = '1.0.0';
          vaObj.videoName = 'hbFriendlyName'; // this will overwrite the ContextData variable a.media.friendlyName
          vaObj.assetDuration = durationInSeconds;
          // use this to override the default asset length of -1 for live streams
          vaObj.debugLogging = false;
          return vaObj;
      }
      ```

   2. Dopo aver creato un&#39;istanza di lettore multimediale, crea un&#39;istanza di tracciamento di Video Analytics e fornisci un riferimento all&#39;istanza di lettore multimediale.
Ricorda quanto segue:

      * Crea sempre una nuova istanza di tracciamento per ogni sessione di riproduzione dei contenuti e rimuovi il riferimento precedente (dopo aver scollegato l&#39;istanza di Media Player).
      * I metadati creati nel passaggio 1 secondario devono essere forniti nel costruttore di Video Analytics Tracker.

         ```js
         var videoAnalyticsMetadata = getVideoAnalyticsMetadata();
         videoAnalyticsProvider = new AdobePSDK.VA.VideoAnalyticsProvider(videoAnalyticsMetadata);
         videoAnalyticsProvider.attachMediaPlayer(player);
         ```
   3. Distruggi il tracker di Video Analytics.
Prima di iniziare una nuova sessione di riproduzione dei contenuti, elimina l’istanza precedente del tracker di video. Dopo aver ricevuto l’evento di completamento del contenuto (o notifica), attendi alcuni minuti prima di eliminare l’istanza di tracciamento video. La distruzione immediata dell’istanza potrebbe interferire con la capacità del tracker di Video Analytics di inviare un ping completo del video.

      ```js
      if (videoAnalyticsProvider) {
          videoAnalyticsProvider.detachMediaPlayer();
          videoAnalyticsProvider = null;
      ```

   4. Contrassegna manualmente il flusso Live/Lineare come completato.
Se hai vari episodi su uno streaming live, puoi contrassegnare manualmente un episodio come completo utilizzando l&#39;API completa. Questo termina la sessione di tracciamento video per l&#39;episodio video corrente e puoi avviare una nuova sessione di tracciamento per l&#39;episodio successivo.
      >[!TIP]
      >
      >Questa API è facoltativa e non è necessaria per il tracciamento video VOD.

      ```js
      if (videoAnalyticsProvider)
      {
         videoAnalyticsProvider.trackVideoComplete();
      videoAnalyticsProvider.detachMediaPlayer();
      videoAnalyticsProvider = null;
      // Create a new instance of VideoAnalyticsProvider to continue tracking.
      }
      ```
