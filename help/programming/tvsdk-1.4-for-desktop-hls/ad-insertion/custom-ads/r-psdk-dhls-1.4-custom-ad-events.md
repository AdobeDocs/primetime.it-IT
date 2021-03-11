---
description: Il lettore TVSDK invia eventi per visualizzare lo stato di caricamento degli annunci personalizzati o per ignorare un annuncio che richiede troppo tempo per essere caricato o presenta errori. Questi eventi sono definiti in events.CustomAdEvents.
title: Eventi di annunci personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# Eventi di annunci personalizzati{#custom-ad-events}

Il lettore TVSDK invia eventi per visualizzare lo stato di caricamento degli annunci personalizzati o per ignorare un annuncio che richiede troppo tempo per essere caricato o presenta errori. Questi eventi sono definiti in events.CustomAdEvents.

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Evento </th> 
   <th colname="col2" class="entry"> Definizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdClickThru  </span> </td> 
   <td colname="col2"> Il numero di volte in cui il visualizzatore ha fatto clic su un annuncio personalizzato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError  </span> </td> 
   <td colname="col2"> Errore nell'annuncio personalizzato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded  </span> </td> 
   <td colname="col2"> L'annuncio personalizzato è stato caricato.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading  </span> </td> 
   <td colname="col2"> L'annuncio personalizzato è in fase di caricamento. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused  </span> </td> 
   <td colname="col2"> L'annuncio personalizzato è stato messo in pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed  </span> </td> 
   <td colname="col2"> L’annuncio personalizzato ha continuato a essere riprodotto dopo una pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPlay  </span> </td> 
   <td colname="col2"> È in corso la riproduzione dell’annuncio personalizzato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress  </span> </td> 
   <td colname="col2"> <p>Il lettore di annunci personalizzato notifica al lettore TVSDK l’avanzamento dell’annuncio personalizzato. &amp;nbsp; </p> <p>Questo evento trasmette <span class="codeph"> currentTime </span> e <span class="codeph"> totalTime </span> dell'annuncio. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> L’annuncio personalizzato ha iniziato la riproduzione e viene visualizzato al visualizzatore.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> La riproduzione dell'annuncio personalizzato è terminata. </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->

