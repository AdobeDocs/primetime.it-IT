---
description: I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.
seo-description: I metodi della classe MediaPlayerItem consentono di ottenere informazioni sul flusso di contenuto rappresentato da un oggetto MediaResource caricato.
seo-title: Attributi di MediaPlayer per accedere alle informazioni di MediaResource
title: Attributi di MediaPlayer per accedere alle informazioni di MediaResource
uuid: d26f39d6-0a6b-4072-b99a-8767a511a846
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '238'
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
   <td colname="1"> Flusso live </td> 
   <td colname="2"> <span class="codeph"> live </span> </td> 
   <td colname="3"> True se il flusso è attivo; false se è VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Sottotitoli codificati </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions </span> </td> 
   <td colname="3"> True se sono disponibili tracce di sottotitoli codificati. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks </span> </td> 
   <td colname="3"> Fornisce un elenco delle tracce di sottotitoli codificati disponibili. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack </span> </td> 
   <td colname="3"> Recupera la traccia dei sottotitoli codificati selezionata con <span class="codeph"> selectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Audio alternativo </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio </span> </td> 
   <td colname="3"> <p>True se il flusso dispone di tracce audio alternative. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks </span> </td> 
   <td colname="3"> Fornisce un elenco delle tracce audio alternative disponibili. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedAudioTrack </span> </td> 
   <td colname="3"> 
    <pre>
      Recupera la traccia audio correntemente selezionata con <span class="codeph"> SelezionaAudioTrack </span>. 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Metadati temporizzati </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata </span> </td> 
   <td colname="3"> True se il flusso ha associato metadati temporizzati. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata </span> </td> 
   <td colname="3"> Fornisce un elenco degli oggetti metadati temporizzati associati al flusso. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Profili multipli (bitrate) </td> 
   <td colname="2" morerows="1"> <span class="codeph"> profili </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> Fornisce un elenco dei profili di bitrate associati a questo flusso. <p>Nota:  Potete recuperare il bitrate per ciascun profilo e l’altezza e la larghezza del profilo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Risorse multimediali </td> 
   <td colname="2"> <span class="codeph"> resource </span> </td> 
   <td colname="3"> Restituisce la risorsa multimediale associata all'elemento. </td> 
  </tr> 
 </tbody> 
</table>

