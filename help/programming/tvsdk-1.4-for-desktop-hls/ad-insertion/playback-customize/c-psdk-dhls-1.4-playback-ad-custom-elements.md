---
description: TVSDK fornisce classi e metodi che possono essere utilizzati per personalizzare il comportamento di riproduzione del contenuto che contiene annunci pubblicitari.
seo-description: TVSDK fornisce classi e metodi che possono essere utilizzati per personalizzare il comportamento di riproduzione del contenuto che contiene annunci pubblicitari.
seo-title: Elementi API per la riproduzione di annunci
title: Elementi API per la riproduzione di annunci
uuid: 61ebbfd7-696c-4a5b-8dbb-682770cd5840
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Elementi API per la riproduzione di annunci{#api-elements-for-ad-playback}

TVSDK fornisce classi e metodi che possono essere utilizzati per personalizzare il comportamento di riproduzione del contenuto che contiene annunci pubblicitari.

I seguenti elementi API sono utili per personalizzare la riproduzione:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Elemento API </th> 
   <th colname="col2" class="entry"> Contenuto che supporta la pubblicità </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdvertisingMetadata</span> </td> 
   <td colname="col2">Controllate se un'interruzione annuncio deve essere contrassegnata come osservata da un visualizzatore e, in caso affermativo, quando contrassegnarla. Imposta e ottieni il criterio controllato utilizzando 
    <ph>
     la proprietà <span class="codeph"> adBreakAsWatched</span> .
    </ph> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Enumera possibili criteri di riproduzione per le interruzioni di annunci. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicy</span> </td> 
   <td colname="col2"> Enumera possibili criteri di riproduzione per gli annunci. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicySelector</span> </td> 
   <td colname="col2"> Interfaccia che consente la personalizzazione del comportamento degli annunci TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DefaultAdPolicySelector</span> </td> 
   <td colname="col2"> Classe che implementa il comportamento TVSDK predefinito. L'applicazione può ignorare questa classe per personalizzare i comportamenti predefiniti senza implementare l'interfaccia completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> localTime</span>. <p>Ora locale della riproduzione, ad eccezione delle interruzioni pubblicitarie inserite. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> searchToLocal</span>. <p>In questo caso, la ricerca si verifica in relazione a un'ora locale nel flusso. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>La posizione virtuale sulla timeline viene convertita nella posizione locale. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> TimelineItem</span> </td> 
   <td colname="col2"> 
    <ul id="ul_99AD34F823DB4F10937EE39DAD0C0B72"> 
     <li id="li_87E2DA15ECE74CFE9C9FBBE8F4B62440"><span class="codeph"> ho guardato</span>. <p>Indica se il visualizzatore ha guardato l’annuncio. </p> </li> 
     <li id="li_A9E5A9CF701C48BC94C93F28C114778D"><span class="codeph"> localRange</span>. <p>La posizione iniziale e la durata di un'interruzione di annuncio o di annuncio rispetto al contenuto originale. </p> </li> 
     <li id="li_070BDA0BF4184863AF44652BD5A0CCEC"><span class="codeph"> virtualRange</span>. <p>La posizione iniziale e la durata di un'interruzione di annuncio o di annuncio sulla timeline virtuale dopo aver considerato tutte le interruzioni di annuncio inserite. </p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

