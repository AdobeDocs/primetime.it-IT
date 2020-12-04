---
description: I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.
seo-description: I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.
seo-title: Metodi MediaPlayer per accedere alle informazioni MediaResource
title: Metodi MediaPlayer per accedere alle informazioni MediaResource
uuid: c2d18f8e-4107-42bc-a975-9b881aadd27b
translation-type: tm+mt
source-git-commit: b9e98ef2b4246fdfd79ebcd91db344c97367d661
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---


# Metodi MediaPlayer per l&#39;accesso alle informazioni MediaResource{#mediaplayer-methods-for-accessing-mediaresource-information}

I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.

<table frame="all" colsep="1" rowsep="1" id="table_77B55D506FE24326A03D97AA087231FF"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> Metodo </th> 
   <th colname="3" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Flusso live  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isLive():Boolean;  </span> </td> 
   <td colname="3"> <p>True se il flusso è attivo; false se è VOD. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Protezione DRM</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isProtected():Boolean;  </span> </td> 
   <td colname="3"> <p>True se il flusso è protetto da DRM. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get drmMetadataInfos(): Vettoriale.&lt;drmmetadatainfo&gt;;  </span> </td> 
   <td colname="3"> <p>Elenca tutti gli oggetti metadati DRM rilevati nel manifest. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Sottotitoli codificati</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasClosedCaptions():Boolean;  </span> </td> 
   <td colname="3"> <p>True se sono disponibili tracce di sottotitoli codificati. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get closedCaptionsTracks():Vector.&lt;closedcaptionstrack&gt;;  </span> </td> 
   <td colname="3"> <p>Fornisce un elenco delle tracce di sottotitoli codificati disponibili. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get selectedClosedCaptionsTrack():ClosedCaptionsTrack  </span> </td> 
   <td colname="3"> <p>Recupera la traccia dei sottotitoli codificati corrente selezionata con <span class="codeph"> SelectClosedCaptionsTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack (closedCaptionsTrack): com.adobe.mediacore.info:ClosedCaptionsTrack )  </span> </td> 
   <td colname="3"> <p>Imposta una traccia con didascalie chiuse come traccia corrente per i sottotitoli codificati. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Tracce audio alternative  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasAlternateAudio():Boolean;  </span> </td> 
   <td colname="3"> <p>True se il flusso dispone di tracce audio alternative. </p> <p>Suggerimento:  La traccia audio principale (predefinita) fa parte dell’elenco di tracce audio alternative. </p> <p>TVSDK per Desktop HLS considera la traccia audio principale come uno degli elementi nell’elenco delle tracce audio alternative. Per questo motivo, l'unico caso in cui <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> restituisce false è quando il flusso non ha alcun audio. Se il contenuto dispone di una sola traccia audio, questo metodo restituisce true e <span class="codeph"> get AudioTracks </span> restituisce un elenco con un singolo elemento (la traccia audio predefinita). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get audioTracks():Vector.&lt;audiotrack&gt;;  </span> </td> 
   <td colname="3"> Fornisce un elenco delle tracce audio alternative disponibili. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get audioTracks():Vector.&lt;audiotrack&gt;;  </span> </td> 
   <td colname="3"> <p>Fornisce un elenco delle tracce audio alternative disponibili. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get selectedAudioTrack():AudioTrack;  </span> </td> 
   <td colname="3"> <p>Recupera la traccia audio selezionata con <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(audioTrack: AudioTrack )  </span> </td> 
   <td colname="3"> <p>Seleziona una traccia audio come traccia audio corrente. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Metadati temporizzati</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasTimedMetadata():Boolean;  </span> </td> 
   <td colname="3"> <p>True se il flusso ha associato metadati temporizzati. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get timedMetadata():Vector.&lt;timedmetadata&gt;;  </span> </td> 
   <td colname="3"> <p>Fornisce un elenco degli oggetti metadati temporizzati associati al flusso. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isDynamic():Boolean;  </span> </td> 
   <td colname="3"> <p>True se il flusso è un flusso MBR (bit rate multiplo). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get profile():Vector.&lt;profile&gt;;  </span> </td> 
   <td colname="3"> <p>Fornisce un elenco dei profili di bitrate associati. Per ciascun profilo, potete recuperarne il bitrate e l’altezza e la larghezza del profilo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Gioco di mattoni  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isTrickPlaySupported():Boolean;  </span> </td> 
   <td colname="3"> <p>True se il lettore supporta avanzamento rapido, riavvolgimento e ripresa. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get availablePlaybackRates():Vector.&lt;number&gt; </span> </td> 
   <td colname="3"> <p>Fornisce l'elenco delle frequenze di riproduzione disponibili nel contesto della funzione "trucco-play". </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Media Player  </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get player():MediaPlayer  </span> </td> 
   <td colname="3"> <p>Restituisce il lettore multimediale attualmente associato al lettore. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Risorse multimediali</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get resource():MediaResource;  </span> </td> 
   <td colname="3"> <p>Restituisce la risorsa multimediale associata all'elemento. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> function get resourceId():int  </span> </td> 
   <td colname="3"> <p>Restituisce l'identificatore multimediale associato all'elemento. </p> </td> 
  </tr> 
 </tbody> 
</table>

