---
description: I metodi della classe MediaPlayerItem ti consentono di ottenere informazioni sul flusso di contenuto rappresentato da un MediaResource caricato.
title: Attributi di MediaPlayer per accedere alle informazioni di MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Attributi di MediaPlayer per accedere alle informazioni di MediaResource{#mediaplayer-attributes-to-access-mediaresource-information}

I metodi della classe MediaPlayerItem ti consentono di ottenere informazioni sul flusso di contenuto rappresentato da un MediaResource caricato.

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
   <td colname="1"> Flusso live </td> 
   <td colname="2"> <span class="codeph"> live  </span> </td> 
   <td colname="3"> True se il flusso è attivo; false se è VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Sottotitoli codificati </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions  </span> </td> 
   <td colname="3"> True se sono disponibili tracce di sottotitoli. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks  </span> </td> 
   <td colname="3"> Fornisce un elenco delle tracce di sottotitoli disponibili. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack  </span> </td> 
   <td colname="3"> Recupera la traccia della didascalia chiusa selezionata con <span class="codeph"> selectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Audio alternativo </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio  </span> </td> 
   <td colname="3"> <p>True se il flusso dispone di tracce audio alternative. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks  </span> </td> 
   <td colname="3"> Fornisce un elenco delle tracce audio alternative disponibili. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedAudioTrack  </span> </td> 
   <td colname="3"> 
    <pre>
      Recupera la traccia audio attualmente selezionata con 
     <span class="codeph"> selectAudioTrack </span>. 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Metadati temporizzati </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata  </span> </td> 
   <td colname="3"> True se il flusso ha associato metadati temporizzati. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata  </span> </td> 
   <td colname="3"> Fornisce un elenco degli oggetti metadati temporizzati associati al flusso. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Profili multipli (bit rate) </td> 
   <td colname="2" morerows="1"> <span class="codeph"> profiles  </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> Fornisce un elenco dei profili di bit rate associati a questo flusso. <p>Nota:  Puoi recuperare il bit rate di ciascun profilo e l’altezza e la larghezza del profilo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Risorsa multimediale </td> 
   <td colname="2"> <span class="codeph"> risorsa  </span> </td> 
   <td colname="3"> Restituisce la risorsa multimediale associata all'elemento. </td> 
  </tr> 
 </tbody> 
</table>

