---
description: Il lettore TVSDK invia gli eventi per visualizzare lo stato di caricamento degli annunci personalizzati o per ignorare un annuncio che richiede troppo tempo o presenta errori. Questi eventi sono definiti in events.CustomAdEvents.
title: Eventi pubblicitari personalizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# Eventi pubblicitari personalizzati{#custom-ad-events}

Il lettore TVSDK invia gli eventi per visualizzare lo stato di caricamento degli annunci personalizzati o per ignorare un annuncio che richiede troppo tempo o presenta errori. Questi eventi sono definiti in events.CustomAdEvents.

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Evento </th> 
   <th colname="col2" class="entry"> Definizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdClickThru </span> </td> 
   <td colname="col2"> Il numero di volte in cui il visualizzatore ha fatto clic su un annuncio personalizzato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError </span> </td> 
   <td colname="col2"> Si è verificato un errore nell’annuncio personalizzato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded </span> </td> 
   <td colname="col2"> L’annuncio personalizzato è stato caricato.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading </span> </td> 
   <td colname="col2"> Caricamento dell’annuncio personalizzato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused </span> </td> 
   <td colname="col2"> L’annuncio personalizzato è stato sospeso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed </span> </td> 
   <td colname="col2"> L’annuncio personalizzato ha continuato a essere riprodotto dopo una pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPlaying </span> </td> 
   <td colname="col2"> Riproduzione dell’annuncio personalizzato in corso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress </span> </td> 
   <td colname="col2"> <p>Il lettore di annunci personalizzati notifica al lettore TVSDK l’avanzamento dell’annuncio personalizzato. &amp;nbsp; </p> <p>Il <span class="codeph"> currentTime </span> e <span class="codeph"> totalTime </span> dell’annuncio vengono passati con questo evento. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> L’annuncio personalizzato ha iniziato la riproduzione e viene visualizzato al visualizzatore.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> La riproduzione dell’annuncio personalizzato è stata completata. </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->
