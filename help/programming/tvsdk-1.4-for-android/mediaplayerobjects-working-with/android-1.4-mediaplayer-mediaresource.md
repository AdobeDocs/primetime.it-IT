---
description: I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.
title: Metodi MediaPlayer per l'accesso alle informazioni MediaResource
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '405'
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
   <td colname="1"> <b>Tag annuncio</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;string&gt; getAdTags() </span> </td> 
   <td colname="3"> <p>Fornisce l’elenco dei tag di annunci utilizzati per il processo di posizionamento degli annunci. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Streaming live</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isLive(); </span> </td> 
   <td colname="3"> <p>True se il flusso è attivo; false se è VOD. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>DRM protetto</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isProtected(); </span> </td> 
   <td colname="3"> <p>True se il flusso è protetto da DRM. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;drmmetadatainfo&gt; getDRMMetadataInfos(); </span> </td> 
   <td colname="3"> <p>Elenca tutti gli oggetti metadati DRM individuati nel manifesto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Sottotitoli</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> valore booleano hasClosedCaptions(); </span> </td> 
   <td colname="3"> <p>True se sono disponibili tracce di sottotitoli. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;closedcaptionstrack&gt; getClosedCationsTracks(); </span> </td> 
   <td colname="3"> <p>Fornisce un elenco delle tracce di sottotitoli. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack ottiene SelectedClosedCaptionsTrack(); </span> </td> 
   <td colname="3"> <p>Recupera la traccia di sottotitoli attualmente selezionata con <span class="codeph"> SelectClosedCaptionsTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> <p>Imposta una traccia sottotitoli come traccia sottotitoli corrente. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Tracce audio alternative</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasAlternateAudio(); </span> </td> 
   <td colname="3"> <p>True se il flusso ha tracce audio alternative. </p> <p>Suggerimento: anche la traccia audio principale (predefinita) fa parte dell'elenco delle tracce audio alternative. </p> <p>TVSDK per Android considera la traccia audio principale come una delle voci dell'elenco delle tracce audio alternative. A causa di questo, l'unico caso in cui <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> restituisce false è quando il flusso non ha alcun audio. Se il contenuto ha una sola traccia audio, questo metodo restituisce true e <span class="codeph"> MediaPlayerItem.getAudioTracks </span> restituisce un elenco con un singolo elemento (la traccia audio predefinita). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;audiotrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> Fornisce un elenco delle tracce audio alternative disponibili. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;audiotrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> <p>Fornisce un elenco delle tracce audio alternative disponibili. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack(); </span> </td> 
   <td colname="3"> <p>Recupera la traccia audio selezionata con <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audio ) </span> </td> 
   <td colname="3"> <p>Seleziona una traccia audio come traccia audio corrente. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Metadati temporizzati</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata() booleano; </span> </td> 
   <td colname="3"> <p>True se al flusso sono associati metadati temporizzati. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;timedmetadata&gt; getTimedMetadata(); </span> </td> 
   <td colname="3"> <p>Fornisce un elenco degli oggetti metadati temporizzati associati al flusso. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isDynamic(); </span> </td> 
   <td colname="3"> <p>True se il flusso è un flusso MBR (Multiple Bit Rate). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt;profile&gt; getProfiles(); </span> </td> 
   <td colname="3"> <p>Fornisce un elenco dei profili di velocità bit associati. Per ogni profilo, puoi recuperarne la velocità in bit e l’altezza e la larghezza. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Trick play</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> valore booleano isTrickPlaySupported(); </span> </td> 
   <td colname="3"> <p>True se il lettore supporta l'avanzamento rapido, il riavvolgimento e la ripresa. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Elenco&lt; Mobile&gt; getAvailablePlaybackRates </span> </td> 
   <td colname="3"> <p>Fornisce l'elenco delle velocità di riproduzione disponibili nel contesto della funzione di riproduzione con trick. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Risorsa multimediale</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource(); </span> </td> 
   <td colname="3"> <p>Restituisce la risorsa multimediale associata a questo elemento. </p> </td> 
  </tr> 
 </tbody> 
</table>
