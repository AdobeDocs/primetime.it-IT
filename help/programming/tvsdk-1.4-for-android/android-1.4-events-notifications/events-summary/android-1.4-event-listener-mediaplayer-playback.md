---
description: TVSDK invia eventi di riproduzione quando si verificano operazioni di riproduzione di contenuti multimediali, ad esempio l’avvio della riproduzione di un video.
title: Eventi di riproduzione
exl-id: 675dd444-d58c-4316-9d62-b64e6433b650
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# Eventi di riproduzione{#playback-events}

TVSDK invia eventi di riproduzione quando si verificano operazioni di riproduzione di contenuti multimediali, ad esempio l’avvio della riproduzione di un video.

Per ricevere notifiche su tutti gli eventi relativi alla riproduzione, registra un’implementazione di `MediaPlayer.PlaybackEventListener`, inclusi i seguenti callback di evento.

<table frame="all" colsep="1" rowsep="1"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Evento </th> 
   <th colname="2" class="entry"> Significato </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Riproduzione</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayComplete%28%29" format="html" scope="external"> onPlayComplete</a> </td> 
   <td colname="2"> È stata raggiunta la fine di un'origine multimediale. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayStart%28%29" format="html" scope="external"> onPlayStart</a> </td> 
   <td colname="2"> La riproduzione di un'origine multimediale è stata avviata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRateSelected%28float%29" format="html" scope="external"> onRateSelected</a> (tasso variabile) </td> 
   <td colname="2"> L’utente o TVSDK ha selezionato una nuova velocità di riproduzione, ad esempio avanzamento rapido, riavvolgimento o ripresa della riproduzione a una velocità normale. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRatePlaying%28float%29" format="html" scope="external"> onRatePlaying</a> (tasso variabile) </td> 
   <td colname="2"> Sullo schermo è visibile una nuova velocità di riproduzione. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Contenuti multimediali</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPrepared%28%29" format="html" scope="external"> onPrepared</a> </td> 
   <td colname="2"> Il lettore multimediale è stato preparato correttamente. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onSizeAvailable%28long,%20long%29" format="html" scope="external"> onSizeAvailable</a> (altezza lunga, larghezza lunga) </td> 
   <td colname="2"> Dimensione del supporto disponibile. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Lettore multimediale</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onStateChanged%28com.adobe.mediacore.MediaPlayer.PlayerState,com.adobe.mediacore.MediaPlayerNotification%29" format="html" scope="external"> onStateChanged</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlayerState.html" format="html" scope="external"> MediaPlayer.PlayerState</a> stato, <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html" format="html" scope="external"> MediaPlayerNotification</a> notifica) </td> 
   <td colname="2"> Lo stato del lettore multimediale è cambiato. L'applicazione deve gestire gli errori in questo callback. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onProfileChanged%28long,%20long%29" format="html" scope="external"> onProfileChanged</a> (profilo lungo, tempo lungo) </td> 
   <td colname="2"> Il profilo corrente del lettore multimediale è stato modificato. Utilizza il <span class="codeph"> Profilo</span> per ottenere il nuovo profilo in fase di riproduzione. Utilizza il <span class="codeph"> tempo</span> per ottenere l'ora in cui si è verificato l'evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>MediaplayerItem</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onUpdated%28%29" format="html" scope="external"> onUpdated</a> </td> 
   <td colname="2">Il lettore multimediale ha aggiornato correttamente il contenuto multimediale in uno dei seguenti casi: 
    <ul> 
     <li>Quando si verifica un aggiornamento del manifesto per una risorsa live.</li> 
     <li>Quando un VOD o una risorsa live presenta sottotitoli codificati e per una traccia di sottotitoli codificati viene rilevata per la prima volta un’attività. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Manifesto e timeline</b></td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimedMetadata%28com.adobe.mediacore.metadata.TimedMetadata%29" format="html" scope="external"> onTimedMetadata</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html" format="html" scope="external"> TimedMetadata</a> timedMetadata) </td> 
   <td colname="2"> Nel manifesto viene individuato un nuovo metadati temporizzati. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated%28%29" format="html" scope="external"> onTimelineUpdated</a> </td> 
   <td colname="2">Il lettore multimediale ha aggiunto o rimosso annunci, quindi presenta una timeline aggiornata. <p>Il manifesto aggiornato per una risorsa live e le vecchie interruzioni pubblicitarie sono state rimosse dalla timeline oppure sono state scoperte nuove opportunità pubblicitarie (cue point). Il lettore multimediale tenta di risolvere e inserire eventuali nuovi annunci nella timeline. </p><p> Utilizza questo evento per verificare se la timeline ha aggiornamenti (VOD non cambia durante la riproduzione). È quindi possibile recuperare la timeline utilizzando <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.html#getTimeline%28%29" format="html" scope="external"> MediaPlayer.getTimeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
