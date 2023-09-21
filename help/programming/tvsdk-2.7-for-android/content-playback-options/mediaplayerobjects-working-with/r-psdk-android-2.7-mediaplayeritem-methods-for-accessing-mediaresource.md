---
description: I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.
title: Metodi MediaPlayerItem per accedere alle informazioni MediaResource
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Metodi MediaPlayerItem per accedere alle informazioni MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.

<table frame="all" colsep="1" rowsep="1" id="table_F6006A9167044AC087A6ECB20B8CCD5D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> Metodo </th> 
   <th colname="3" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Tag annuncio</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;string&gt; getAdTags() </span> </td> 
   <td colname="3"> Fornisce l’elenco dei tag di annunci utilizzati per il processo di posizionamento degli annunci. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Streaming live</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isLive(); </span> </td> 
   <td colname="3"> True se il flusso è attivo; false se è VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>DRM protetto</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isProtected(); </span> </td> 
   <td colname="3"> True se il flusso è protetto da DRM. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;drmmetadatainfo&gt; getDRMMetadataInfos(); </span> </td> 
   <td colname="3"> Elenca tutti gli oggetti metadati DRM individuati nel manifesto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Sottotitoli</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> valore booleano hasClosedCaptions(); </span> </td> 
   <td colname="3"> True se sono disponibili tracce di sottotitoli. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;closedcaptionstrack&gt; getClosedCationsTracks(); </span> </td> 
   <td colname="3"> Fornisce un elenco delle tracce di sottotitoli. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack ottiene SelectedClosedCaptionsTrack(); </span> </td> 
   <td colname="3"> Recupera la traccia di sottotitoli attualmente selezionata con <span class="codeph"> SelectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> Imposta una traccia sottotitoli come traccia sottotitoli corrente. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Tracce audio alternative</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasAlternateAudio(); </span> </td> 
   <td colname="3"> True se il flusso ha tracce audio alternative. <p>Nota: anche la traccia audio principale (predefinita) fa parte dell'elenco delle tracce audio alternative. </p> <p>TVSDK per Android considera la traccia audio principale come una delle voci dell'elenco delle tracce audio alternative. A causa di questo, l'unico caso in cui <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> restituisce false è quando il flusso non ha alcun audio. Se il contenuto ha una sola traccia audio, questo metodo restituisce true e <span class="codeph"> MediaPlayerItem.getAudioTracks </span> restituisce un elenco con un singolo elemento (la traccia audio predefinita). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;audiotrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> Fornisce un elenco delle tracce audio alternative disponibili. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack(); </span> </td> 
   <td colname="3"> Recupera la traccia audio selezionata con <span class="codeph"> selectAudioTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audio ) </span> </td> 
   <td colname="3"> Seleziona una traccia audio come traccia audio corrente. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Metadati temporizzati</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata() booleano; </span> </td> 
   <td colname="3"> True se al flusso sono associati metadati temporizzati. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;timedmetadata&gt; getTimedMetadata(); </span> </td> 
   <td colname="3"> Fornisce un elenco degli oggetti metadati temporizzati associati al flusso. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Profili multipli (velocità bit)</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isDynamic(); </span> </td> 
   <td colname="3"> True se il flusso è un flusso MBR (Multiple Bit Rate). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;profile&gt; getProfiles(); </span> </td> 
   <td colname="3"> Fornisce un elenco dei profili di velocità bit associati. Per ogni profilo, puoi recuperarne la velocità in bit e l’altezza e la larghezza. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Profilo getSelectedProfile() </span> </td> 
   <td colname="3"> Recupera il profilo attualmente selezionato. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Trick play</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> valore booleano isTrickPlaySupported(); </span> </td> 
   <td colname="3"> True se il lettore supporta l'avanzamento rapido, il riavvolgimento e la ripresa. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt; Mobile&gt; getAvailablePlaybackRates() </span> </td> 
   <td colname="3"> Fornisce l'elenco delle velocità di riproduzione disponibili nel contesto della funzione di riproduzione con trick. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Float getSelectedPlaybackRate() </span> </td> 
   <td colname="3"> Recupera la velocità di riproduzione attualmente selezionata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig() </span> </td> 
   <td colname="3"> Restituisce il valore <span class="codeph"> MediaPlayerItemConfig </span> istanza associata a questo elemento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Risorsa multimediale</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource(); </span> </td> 
   <td colname="3"> Restituisce la risorsa multimediale associata a questo elemento. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId() </span> </td> 
   <td colname="3"> Restituisce l'identificatore multimediale associato all'elemento. Questo ID viene impostato quando l'elemento viene caricato utilizzando <span class="codeph"> MediaPlayerItemLoader.load </span>. </td> 
  </tr> 
 </tbody> 
</table>
