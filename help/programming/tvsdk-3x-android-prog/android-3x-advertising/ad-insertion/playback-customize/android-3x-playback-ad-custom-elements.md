---
description: TVSDK fornisce classi e metodi che è possibile utilizzare per personalizzare il comportamento di riproduzione dei contenuti che contengono annunci pubblicitari.
title: Elementi API per la riproduzione di annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Elementi API per la riproduzione di annunci {#api-elements-for-ad-playback}

TVSDK fornisce classi e metodi che è possibile utilizzare per personalizzare il comportamento di riproduzione dei contenuti che contengono annunci pubblicitari.

I seguenti elementi API sono utili per personalizzare la riproduzione:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Elemento API </b></th> 
   <th colname="col2" class="entry"> <b>Contenuti che supportano la pubblicità</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdvertisingMetadata </span> </td> 
   <td colname="col2">Controlla se un’interruzione pubblicitaria deve essere contrassegnata come se fosse stata guardata da un visualizzatore e, in caso affermativo, quando contrassegnarla. Imposta e ottieni la policy controllata utilizzando <span class="codeph"> setAdBreakAsWatched</span> e <span class="codeph"> getAdBreakAsWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Enumera i possibili criteri di riproduzione per le interruzioni pubblicitarie. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicy</span> </td> 
   <td colname="col2"> Enumera i possibili criteri di riproduzione per gli annunci. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicySelector </span> </td> 
   <td colname="col2"> Interfaccia che consente di personalizzare il comportamento degli annunci TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> DefaultAdPolicySelector </span> </td> 
   <td colname="col2"> Classe che implementa il comportamento TVSDK predefinito. L’applicazione può eseguire l’override di questa classe per personalizzare i comportamenti predefiniti senza implementare l’interfaccia completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="apiname"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span> <p>Si tratta dell’ora locale della riproduzione, escluse le interruzioni pubblicitarie inserite. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekToLocal</span>. <p>In questo caso, la ricerca si verifica in relazione a un’ora locale nel flusso. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>La posizione virtuale sulla timeline viene convertita nella posizione locale. </p> </li> 
    </ul> <p>Importante:  <span class="codeph"> getLocalTime</span> in <span class="codeph"> MediaPlayer</span> restituisce il tempo corrente relativo al contenuto originale, senza annunci uniti in modo dinamico. <span class="codeph"> getLocalTime</span> in <span class="codeph"> AdBreak</span> restituisce l’ora di inizio dell’interruzione relativa al contenuto originale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> isWatched</span> proprietà. Indica se il visualizzatore ha guardato l’annuncio. </td> 
  </tr> 
 </tbody> 
</table>
