---
description: TVSDK fornisce classi e metodi che è possibile utilizzare per personalizzare il comportamento di riproduzione dei contenuti che contengono annunci pubblicitari.
title: Elementi API per la riproduzione di annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Elementi API per la riproduzione di annunci{#api-elements-for-ad-playback}

TVSDK fornisce classi e metodi che è possibile utilizzare per personalizzare il comportamento di riproduzione dei contenuti che contengono annunci pubblicitari.

I seguenti elementi API sono utili per personalizzare la riproduzione:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Elemento API </th> 
   <th colname="col2" class="entry"> Contenuti che supportano la pubblicità </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdvertisingMetadata</span> </td> 
   <td colname="col2">Controlla se un’interruzione pubblicitaria deve essere contrassegnata come se fosse stata guardata da un visualizzatore e, in caso affermativo, quando contrassegnarla. Imposta e ottieni la policy controllata utilizzando 
    <pre>
     il 
     <span class="codeph"> adBreakAsWatched</span> proprietà.
    </pre> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Enumera i possibili criteri di riproduzione per le interruzioni pubblicitarie. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicy</span> </td> 
   <td colname="col2"> Enumera i possibili criteri di riproduzione per gli annunci. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicySelector</span> </td> 
   <td colname="col2"> Interfaccia che consente di personalizzare il comportamento degli annunci TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DefaultAdPolicySelector</span> </td> 
   <td colname="col2"> Classe che implementa il comportamento TVSDK predefinito. L’applicazione può eseguire l’override di questa classe per personalizzare i comportamenti predefiniti senza implementare l’interfaccia completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> localTime</span>. <p>Si tratta dell’ora locale della riproduzione, escluse le interruzioni pubblicitarie inserite. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocal</span>. <p>In questo caso, la ricerca si verifica in relazione a un’ora locale nel flusso. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>La posizione virtuale sulla timeline viene convertita nella posizione locale. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> TimelineItem</span> </td> 
   <td colname="col2"> 
    <ul id="ul_99AD34F823DB4F10937EE39DAD0C0B72"> 
     <li id="li_87E2DA15ECE74CFE9C9FBBE8F4B62440"><span class="codeph"> guardato</span>. <p>Indica se il visualizzatore ha guardato l’annuncio. </p> </li> 
     <li id="li_A9E5A9CF701C48BC94C93F28C114778D"><span class="codeph"> localRange</span>. <p>La posizione di partenza e la durata di un’interruzione pubblicitaria o di un annuncio rispetto al contenuto originale. </p> </li> 
     <li id="li_070BDA0BF4184863AF44652BD5A0CCEC"><span class="codeph"> virtualRange</span>. <p>La posizione di partenza e la durata di un’interruzione pubblicitaria o di un annuncio sulla timeline virtuale dopo aver considerato tutte le interruzioni pubblicitarie inserite. </p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
