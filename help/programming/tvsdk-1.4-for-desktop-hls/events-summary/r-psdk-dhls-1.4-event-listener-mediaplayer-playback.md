---
description: L’applicazione può monitorare l’attività nel lettore e il cambiamento dello stato del lettore mediante l’ascolto degli eventi inviati da TVSDK.
title: Eventi di riproduzione
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# Eventi di riproduzione {#playback-events}

L’applicazione può monitorare l’attività nel lettore e il cambiamento dello stato del lettore mediante l’ascolto degli eventi inviati da TVSDK.

TVSDK invia eventi di riproduzione quando si verificano operazioni di riproduzione di contenuti multimediali, ad esempio l’avvio della riproduzione di un video. Per ricevere notifiche su tutti gli eventi relativi alla riproduzione, registra i listener con `MediaPlayer` per i seguenti eventi.

<table frame="all" colsep="1" rowsep="1" id="table_922EEA3DE0BD47BA982E11F890CA0A6B"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Evento </th> 
   <th colname="2" class="entry"> Significato </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Riproduzione</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_SELECTED" format="html" scope="external"> RATE_SELECTED</a> </td> 
   <td colname="2"> L’utente o TVSDK ha selezionato una nuova velocità di riproduzione, ad esempio avanzamento rapido, riavvolgimento o ripresa della riproduzione a una velocità normale. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RIPRODUCI_ZIONE</a> </td> 
   <td colname="2"> Sullo schermo è visibile una nuova velocità di riproduzione. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> ORA_MODIFICATA</a> </td> 
   <td colname="2"> La posizione corrente della testina di riproduzione del contenuto multimediale è cambiata. Inviato periodicamente quando l’ora corrente è cambiata, ogni 250 ms o più. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Lettore multimediale</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento di modifica MediaPlayerStatus.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATO_MODIFICATO</a> </td> 
   <td colname="2"> Lo stato del lettore multimediale è cambiato. L'applicazione deve gestire gli errori nel callback di questo evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ProfileEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> PROFILE_CHANGED</a> </td> 
   <td colname="2">Il profilo corrente del lettore multimediale è stato modificato. Utilizza il <span class="codeph"> ProfileEvent.profile</span> per ottenere il nuovo profilo in fase di riproduzione. Utilizza il <span class="codeph"> tempo</span> per ottenere l'ora in cui si è verificato l'evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ELEMENTO_CREATO</a> </td> 
   <td colname="2">A <span class="codeph"> MediaPlayerItem</span> è stato creato. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> ELEMENTO_AGGIORNATO</a> </td> 
   <td colname="2">Il lettore multimediale ha aggiornato correttamente il contenuto multimediale in uno dei seguenti casi: 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">Quando si verifica un aggiornamento del manifesto per una risorsa live. </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">Quando un VOD o una risorsa live presenta sottotitoli codificati e per una traccia di sottotitoli codificati viene rilevata per la prima volta un’attività. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Sottotitoli e audio</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> DIDASCALIA_AGGIORNATA</a> </td> 
   <td colname="2">È stata rilevata una nuova traccia di sottotitoli nel flusso multimediale e nel <span class="codeph"> closedCaptionsTracks</span> raccolta aggiornata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifesto e timeline</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">TimelineEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> TIMELINE_UPDATED</a> </td> 
   <td colname="2">Il lettore multimediale ha aggiunto o rimosso annunci, quindi presenta una timeline aggiornata. <p>Il manifesto aggiornato per una risorsa live e le vecchie interruzioni pubblicitarie sono state rimosse dalla timeline oppure sono state scoperte nuove opportunità pubblicitarie (cue point). Il lettore multimediale tenta di risolvere e inserire eventuali nuovi annunci nella timeline. </p> <p> Utilizza questo evento per verificare se la timeline ha aggiornamenti (VOD non cambia durante la riproduzione). È quindi possibile recuperare la timeline utilizzando <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
