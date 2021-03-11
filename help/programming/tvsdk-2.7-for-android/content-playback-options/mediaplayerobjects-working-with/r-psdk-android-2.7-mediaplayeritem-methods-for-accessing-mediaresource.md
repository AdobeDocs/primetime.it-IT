---
description: I metodi della classe MediaPlayerItem ti consentono di ottenere informazioni sul flusso di contenuto rappresentato da un MediaResource caricato.
title: Metodi MediaPlayerItem per accedere alle informazioni di MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---


# Metodi MediaPlayerItem per accedere alle informazioni di MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

I metodi della classe MediaPlayerItem ti consentono di ottenere informazioni sul flusso di contenuto rappresentato da un MediaResource caricato.

<table frame="all" colsep="1" rowsep="1" id="table_F6006A9167044AC087A6ECB20B8CCD5D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> Metodo </th> 
   <th colname="3" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Tag annunci</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;string&gt; ListgetAdTags()  </span> </td> 
   <td colname="3"> Fornisce l'elenco dei tag degli annunci utilizzati per il processo di posizionamento degli annunci. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Flusso live</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isLive();  </span> </td> 
   <td colname="3"> True se il flusso è attivo; false se è VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>DRM protetto</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isProtected();  </span> </td> 
   <td colname="3"> True se il flusso è protetto DRM. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;drmmetadatainfo&gt; ListgetDRMMetadataInfos();  </span> </td> 
   <td colname="3"> Elenca tutti gli oggetti metadati DRM scoperti nel manifesto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Sottotitoli codificati</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasClosedCaptions();  </span> </td> 
   <td colname="3"> True se sono disponibili tracce di sottotitoli. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;closedcaptionstrack&gt; ListgetClosedCationsTracks();  </span> </td> 
   <td colname="3"> Fornisce un elenco delle tracce di sottotitoli disponibili. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SelectedClosedCaptionsTrack();  </span> </td> 
   <td colname="3"> Recupera la traccia corrente della didascalia chiusa selezionata con <span class="codeph"> SelectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack)  </span> </td> 
   <td colname="3"> Imposta una traccia a didascalia chiusa come traccia corrente a didascalia chiusa. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Tracce audio alternative</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasAlternateAudio();  </span> </td> 
   <td colname="3"> True se il flusso dispone di tracce audio alternative. <p>Nota:  La traccia audio principale (predefinita) fa anche parte dell’elenco di tracce audio alternative. </p> <p>TVSDK per Android considera la traccia audio principale come uno degli elementi nell’elenco di tracce audio alternative. Per questo motivo, l'unico caso in cui <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> restituisce false è quando il flusso non ha alcun audio. Se il contenuto dispone di una sola traccia audio, questo metodo restituisce true e <span class="codeph"> MediaPlayerItem.getAudioTracks </span> restituisce un elenco con un singolo elemento (la traccia audio predefinita). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;audiotrack&gt; ListgetAudioTracks();  </span> </td> 
   <td colname="3"> Fornisce un elenco delle tracce audio alternative disponibili. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack();  </span> </td> 
   <td colname="3"> Recupera la traccia audio selezionata con <span class="codeph"> selectAudioTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack )  </span> </td> 
   <td colname="3"> Seleziona una traccia audio come traccia audio corrente. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Metadati temporizzati</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasTimedMetadata();  </span> </td> 
   <td colname="3"> True se il flusso ha associato metadati temporizzati. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;timedmetadata&gt; ListgetTimedMetadata();  </span> </td> 
   <td colname="3"> Fornisce un elenco degli oggetti metadati temporizzati associati al flusso. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Profili multipli (bit rate)</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isDynamic();  </span> </td> 
   <td colname="3"> True se il flusso è un flusso a bit rate multiplo (MBR). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;profile&gt; ListgetProfiles();  </span> </td> 
   <td colname="3"> Fornisce un elenco dei profili di bit rate associati. Per ciascun profilo, puoi recuperarne il bit rate e l’altezza e la larghezza del profilo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Profilo getSelectedProfile()  </span> </td> 
   <td colname="3"> Recupera il profilo attualmente selezionato. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Gioco di mattoni</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> isTrickPlaySupported() booleano;  </span> </td> 
   <td colname="3"> True se il lettore supporta l'avanzamento rapido, il riavvolgimento e la ripresa. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt; Float=""&gt; ListgetAvailablePlaybackRates()  </span> </td> 
   <td colname="3"> Fornisce l'elenco delle velocità di riproduzione disponibili nel contesto della funzione di riproduzione a forma di trucco. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Mobile getSelectedPlaybackRate()  </span> </td> 
   <td colname="3"> Recupera la velocità di riproduzione attualmente selezionata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig()  </span> </td> 
   <td colname="3"> Restituisce l'istanza <span class="codeph"> MediaPlayerItemConfig </span> associata a questo elemento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Risorsa multimediale</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource();  </span> </td> 
   <td colname="3"> Restituisce la risorsa multimediale associata all'elemento. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId()  </span> </td> 
   <td colname="3"> Restituisce l'identificatore multimediale associato all'elemento. Questo ID viene impostato quando l'elemento viene caricato utilizzando <span class="codeph"> MediaPlayerItemLoader.load </span>. </td> 
  </tr> 
 </tbody> 
</table>
