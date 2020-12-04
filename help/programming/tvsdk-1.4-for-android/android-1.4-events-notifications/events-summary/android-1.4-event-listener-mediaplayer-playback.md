---
description: TVSDK invia eventi di riproduzione quando si verificano operazioni di riproduzione per contenuti multimediali, ad esempio un video che inizia la riproduzione.
seo-description: TVSDK invia eventi di riproduzione quando si verificano operazioni di riproduzione per contenuti multimediali, ad esempio un video che inizia la riproduzione.
seo-title: Eventi di riproduzione
title: Eventi di riproduzione
uuid: 809a8e0e-f4d8-4013-b04a-49fb93d7ca8a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Eventi di riproduzione{#playback-events}

TVSDK invia eventi di riproduzione quando si verificano operazioni di riproduzione per contenuti multimediali, ad esempio un video che inizia la riproduzione.

Per ricevere notifiche su tutti gli eventi relativi alla riproduzione, registrate un&#39;implementazione di `MediaPlayer.PlaybackEventListener`, compresi i callback di evento seguenti.

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
   <td colname="2"> È stata raggiunta la fine di una fonte multimediale. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayStart%28%29" format="html" scope="external"> onPlayStart</a> </td> 
   <td colname="2"> La riproduzione di un'origine multimediale è iniziata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRateSelected%28float%29" format="html" scope="external"> onRateSelected</a> (rate mobile) </td> 
   <td colname="2"> L’utente o TVSDK ha selezionato una nuova frequenza di riproduzione, ad esempio avanzamento rapido, riavvolgimento o ripresa della riproduzione a una velocità normale. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRatePlaying%28float%29" format="html" scope="external"> onRatePlaying</a> (rate mobile) </td> 
   <td colname="2"> Sullo schermo è visibile una nuova frequenza di riproduzione. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Media</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPrepared%28%29" format="html" scope="external"> onPrepared</a> </td> 
   <td colname="2"> Il lettore multimediale ha preparato con successo il supporto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onSizeAvailable%28long,%20long%29" format="html" scope="external"> onSizeAvailable</a> (altezza lunga, larghezza lunga) </td> 
   <td colname="2"> Sono disponibili le dimensioni del supporto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Media Player</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onStateChanged%28com.adobe.mediacore.MediaPlayer.PlayerState,com.adobe.mediacore.MediaPlayerNotification%29" format="html" scope="external"> onStateChanged</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlayerState.html" format="html" scope="external"> MediaPlayer.</a> PlayerState,  <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html" format="html" scope="external"> </a> MediaPlayerNotificationnotification) </td> 
   <td colname="2"> Lo stato del lettore multimediale è cambiato. L’applicazione deve gestire gli errori in questo callback. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onProfileChanged%28long,%20long%29" format="html" scope="external"> onProfileChanged</a> (profilo lungo, tempo lungo) </td> 
   <td colname="2"> Il profilo corrente del lettore multimediale è cambiato. Utilizzare la proprietà <span class="codeph"> Profile</span> per ottenere il nuovo profilo in fase di riproduzione. Utilizzare la proprietà <span class="codeph"> time</span> per ottenere l'ora in cui si è verificato l'evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>MediaplayerItem</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onUpdated%28%29" format="html" scope="external"> onUpdated</a> </td> 
   <td colname="2">Il lettore multimediale ha aggiornato il supporto in uno dei seguenti casi: 
    <ul> 
     <li>Quando si verifica un aggiornamento manifesto per una risorsa live.</li> 
     <li>Quando un VOD o una risorsa live presenta sottotitoli codificati e l’attività viene scoperta per la prima volta per una traccia di sottotitoli codificati. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Manifesto e Timeline</b></td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimedMetadata%28com.adobe.mediacore.metadata.TimedMetadata%29" format="html" scope="external"> onTimedMetadata</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html" format="html" scope="external"> </a> TimedMetadatimedMetadata) </td> 
   <td colname="2"> Nel file manifesto vengono rilevati nuovi metadati temporizzati. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated%28%29" format="html" scope="external"> onTimelineUpdated</a> </td> 
   <td colname="2">Il lettore multimediale ha aggiunto o rimosso gli annunci, pertanto dispone di una timeline aggiornata. <p>Il manifesto aggiornato per una risorsa live e le vecchie interruzioni pubblicitarie sono state rimosse dalla timeline oppure sono state scoperte nuove opportunità (cue point). Il lettore multimediale tenta di risolvere e inserire nuovi annunci sulla timeline. </p><p> Usare questo evento per verificare se la timeline contiene aggiornamenti (il VOD non cambia durante la riproduzione). Potete quindi recuperare la timeline utilizzando <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.html#getTimeline%28%29" format="html" scope="external"> MediaPlayer.getTimeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
