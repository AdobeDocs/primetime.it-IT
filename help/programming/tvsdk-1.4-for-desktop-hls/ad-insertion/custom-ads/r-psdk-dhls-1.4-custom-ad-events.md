---
description: Il lettore TVSDK invia eventi per visualizzare lo stato di caricamento personalizzato degli annunci o per ignorare un annuncio pubblicitario che richiede troppo tempo per essere caricato o presenta errori. Questi eventi sono definiti in events.CustomAdEvents.
seo-description: Il lettore TVSDK invia eventi per visualizzare lo stato di caricamento personalizzato degli annunci o per ignorare un annuncio pubblicitario che richiede troppo tempo per essere caricato o presenta errori. Questi eventi sono definiti in events.CustomAdEvents.
seo-title: Eventi annunci personalizzati
title: Eventi annunci personalizzati
uuid: 78e2ccf4-5943-4c60-84be-623182d9a300
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Eventi annunci personalizzati{#custom-ad-events}

Il lettore TVSDK invia eventi per visualizzare lo stato di caricamento personalizzato degli annunci o per ignorare un annuncio pubblicitario che richiede troppo tempo per essere caricato o presenta errori. Questi eventi sono definiti in events.CustomAdEvents.

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
   <td colname="col2"> Si è verificato un errore con l'annuncio personalizzato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded  </span> </td> 
   <td colname="col2"> L'annuncio personalizzato è stato caricato.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading  </span> </td> 
   <td colname="col2"> Caricamento dell'annuncio personalizzato in corso. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused  </span> </td> 
   <td colname="col2"> L'annuncio personalizzato è stato messo in pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed  </span> </td> 
   <td colname="col2"> L'annuncio personalizzato è stato riprodotto dopo una pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPlay  </span> </td> 
   <td colname="col2"> Viene riprodotto l'annuncio personalizzato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress  </span> </td> 
   <td colname="col2"> <p>Il lettore annunci personalizzato notifica al lettore TVSDK l'avanzamento dell'annuncio personalizzato. &amp;nbsp; </p> <p>Il <span class="codeph"> currentTime </span> e <span class="codeph"> totalTime </span> dell'annuncio vengono passati con questo evento. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> La riproduzione dell'annuncio personalizzato è iniziata e viene visualizzata al visualizzatore.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> La riproduzione dell'annuncio personalizzato è terminata. </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->

