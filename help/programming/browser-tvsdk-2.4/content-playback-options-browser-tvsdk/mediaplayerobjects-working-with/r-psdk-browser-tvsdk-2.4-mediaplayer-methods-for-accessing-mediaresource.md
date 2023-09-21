---
description: I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.
title: Attributi di MediaPlayer per accedere alle informazioni di MediaResource
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Attributi di MediaPlayer per accedere alle informazioni di MediaResource{#mediaplayer-attributes-to-access-mediaresource-information}

I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.

<table frame="all" colsep="1" rowsep="1" id="table_46225307CA5B4BB1869576E0B9141E38"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Finalità </th> 
   <th colname="2" class="entry"> Attributo </th> 
   <th colname="3" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Streaming live </td> 
   <td colname="2"> <span class="codeph"> live </span> </td> 
   <td colname="3"> True se il flusso è attivo; false se è VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Sottotitoli </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions </span> </td> 
   <td colname="3"> True se sono disponibili tracce di sottotitoli. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks </span> </td> 
   <td colname="3"> Fornisce un elenco delle tracce di sottotitoli. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack </span> </td> 
   <td colname="3"> Recupera la traccia sottotitoli selezionata con <span class="codeph"> selectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Audio alternativo </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio </span> </td> 
   <td colname="3"> <p>True se il flusso ha tracce audio alternative. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks </span> </td> 
   <td colname="3"> Fornisce un elenco delle tracce audio alternative disponibili. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedAudioTrack </span> </td> 
   <td colname="3"> 
    <pre>
      Recupera la traccia audio attualmente selezionata con 
     <span class="codeph"> selectAudioTrack </span>. 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Metadati temporizzati </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata </span> </td> 
   <td colname="3"> True se al flusso sono associati metadati temporizzati. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata </span> </td> 
   <td colname="3"> Fornisce un elenco degli oggetti metadati temporizzati associati al flusso. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Profili multipli (velocità bit) </td> 
   <td colname="2" morerows="1"> <span class="codeph"> profili </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> Fornisce un elenco dei profili di velocità bit associati a questo flusso. <p>Nota: è possibile recuperare la velocità bit per ciascun profilo e l'altezza e la larghezza del profilo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Risorsa multimediale </td> 
   <td colname="2"> <span class="codeph"> resource </span> </td> 
   <td colname="3"> Restituisce la risorsa multimediale associata a questo elemento. </td> 
  </tr> 
 </tbody> 
</table>
