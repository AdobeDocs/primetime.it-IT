---
description: L’applicazione può monitorare l’attività nel lettore e lo stato di modifica del lettore ascoltando gli eventi inviati da TVSDK.
title: Eventi di riproduzione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Eventi di riproduzione {#playback-events}

L’applicazione può monitorare l’attività nel lettore e lo stato di modifica del lettore ascoltando gli eventi inviati da TVSDK.

TVSDK invia eventi di riproduzione quando si verificano operazioni di riproduzione di contenuti multimediali, ad esempio un video che inizia la riproduzione. Per ricevere notifiche su tutti gli eventi relativi alla riproduzione, registra i listener con l&#39;oggetto `MediaPlayer` per i seguenti eventi.

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
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> Sullo schermo è visibile una nuova velocità di riproduzione. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_CHANGED</a> </td> 
   <td colname="2"> L'attuale posizione del playhead del supporto è cambiata. Inviato periodicamente quando l’ora corrente è cambiata, ogni 250 ms o più. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Media Player</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ChangeEvent di MediaPlayerStatus.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATUS_CHANGED</a> </td> 
   <td colname="2"> Lo stato del lettore multimediale è cambiato. L'applicazione deve gestire gli errori nel callback di questo evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ProfileEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> PROFILE_CHANGED</a> </td> 
   <td colname="2">Il profilo corrente del lettore multimediale è cambiato. Utilizza la proprietà <span class="codeph"> ProfileEvent.profile</span> per ottenere il nuovo profilo in corso di riproduzione. Utilizzare la proprietà <span class="codeph"> time</span> per ottenere l'ora in cui si è verificato l'evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_CREATED</a> </td> 
   <td colname="2">È stato creato un <span class="codeph"> MediaPlayerItem</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> ITEM_AGGIORNATO</a> </td> 
   <td colname="2">Il lettore multimediale ha aggiornato correttamente il contenuto multimediale in uno di questi casi: 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">Quando si verifica un aggiornamento manifesto per una risorsa live. </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">Quando un VOD o una risorsa live presenta sottotitoli codificati e l’attività viene scoperta per la prima volta per una traccia di sottotitoli codificati. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Sottotitoli e audio</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> CAPTION_AGGIORNATO</a> </td> 
   <td colname="2">È stata rilevata una nuova traccia di sottotitoli codificati nel flusso multimediale e la raccolta <span class="codeph"> closedCaptionsTracks</span> è stata aggiornata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifesto e Timeline</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">TimelineEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> TIMELINE_AGGIORNATO</a> </td> 
   <td colname="2">Il lettore multimediale ha aggiunto o rimosso gli annunci, quindi dispone di una timeline aggiornata. <p>Il manifesto aggiornato per una risorsa live e le vecchie interruzioni pubblicitarie sono state rimosse dalla timeline o sono state scoperte nuove opportunità pubblicitarie (punti di cue). Il lettore multimediale cerca di risolvere e inserire nuovi annunci sulla timeline. </p> <p> Usare questo evento per verificare se la timeline presenta aggiornamenti (VOD non cambia durante la riproduzione). È quindi possibile recuperare la timeline utilizzando <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

