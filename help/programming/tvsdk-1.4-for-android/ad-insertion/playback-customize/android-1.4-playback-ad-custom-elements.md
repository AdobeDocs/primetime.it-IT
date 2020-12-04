---
description: TVSDK fornisce classi e metodi che possono essere utilizzati per personalizzare il comportamento di riproduzione del contenuto che contiene annunci pubblicitari.
seo-description: TVSDK fornisce classi e metodi che possono essere utilizzati per personalizzare il comportamento di riproduzione del contenuto che contiene annunci pubblicitari.
seo-title: Elementi API per la riproduzione di annunci
title: Elementi API per la riproduzione di annunci
uuid: 6d0ab181-9c50-431f-97bf-32e6684a7df1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Elementi API per la riproduzione di annunci {#api-elements-for-ad-playback}

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
   <td colname="col2">Controllate se un'interruzione annuncio deve essere contrassegnata come osservata da un visualizzatore e, in caso affermativo, quando contrassegnarla. Impostare e ottenere il criterio controllato utilizzando <span class="codeph"> setAdBreakAsWatched</span> e <span class="codeph"> getAdBreakAsWatched</span>. </td> 
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
   <td colname="col1"><span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span>. <p>Ora locale della riproduzione, ad eccezione delle interruzioni pubblicitarie inserite. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> searchToLocal</span>. <p>In questo caso, la ricerca si verifica in relazione a un'ora locale nel flusso. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>La posizione virtuale sulla timeline viene convertita nella posizione locale. </p> </li> 
    </ul> <p>Importante:  <span class="codeph"> getLocalTime</span> in <span class="codeph"> MediaPlayer</span> restituisce l'ora corrente relativa al contenuto originale, senza annunci con giunzione dinamica. <span class="codeph"> </span> getLocalTimein  <span class="codeph"> </span> AdBreakfast restituisce l'ora di inizio dell'interruzione in relazione al contenuto originale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> </span> isWatchedproperty. Indica se il visualizzatore ha guardato l’annuncio. </td> 
  </tr> 
 </tbody> 
</table>

