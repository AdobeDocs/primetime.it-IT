---
title: Modalità di segnalazione e intervallo di tempo
description: Modalità di segnalazione e intervallo di tempo
copied-description: true
exl-id: ccaf345f-63f2-42f1-8558-65c7e0dffa89
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Modalità di segnalazione e intervallo di tempo {#signaling-mode-and-time-range}

<table> 
 <thead> 
  <tr> 
   <th class="entry"> </th> 
   <th class="entry"> CONTRASSEGNA </th> 
   <th class="entry"> DELETE </th> 
   <th class="entry"> SOSTITUISCI </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Generatore opportunità intervallo personalizzato </span> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
    &nbsp;range.end) 
    </code> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
     &nbsp;range.end) 
    </code> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
      &nbsp;range.end,&nbsp; 
      &nbsp;replaceDuration) 
    </code> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> ServerMap </span> Modalità di segnalazione </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement(&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.MARK&nbsp;); 
    </code> </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement(&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.DELETE&nbsp;); 
    </code> </td> 
   <td> N/D (modalità di segnalazione automatica CustomRange) </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> ManifestCue </span> Modalità di segnalazione </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.MARK 
     ); 
    </code> </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.DELETE 
     ); 
    </code> </td> 
   <td> N/D (modalità di segnalazione automatica CustomRange) </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> CustomRange </span> Modalità di segnalazione </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.MARK 
     ); 
    </code> </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.DELETE 
     ); 
    </code> </td> 
   <td> 
    <code>
      placement1&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.MARK 
     ); 
     placement2&nbsp;=&nbsp;placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement(/ 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.MID_ROLL( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.PRE_ROLL), 
     &nbsp;&nbsp;&nbsp;&nbsp;rangeDuration, 
     &nbsp;&nbsp;&nbsp;&nbsp;placementMode 
     ); 
    </code> </td> 
  </tr> 
 </tbody> 
</table>

<table> 
 <thead> 
  <tr> 
   <th class="entry"> </th> 
   <th class="entry"> CONTRASSEGNA </th> 
   <th class="entry"> DELETE </th> 
   <th class="entry"> SOSTITUISCI </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> AdSignalingMode OpportunityGenerator </span> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
     &nbsp;range.end) 
    </code> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
     &nbsp;range.end) 
    </code> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
     &nbsp;range.end,&nbsp; 
     &nbsp;replaceDuration) 
    </code> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> ServerMap </span> Modalità di segnalazione </td> 
   <td> Non presente (annuncio disabilitato). </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;new&nbsp;Placement( 
     PlacementType.SERVER_MAP, 
     Placement.UNKNOWN_TIME, 
     Placement.UNKNOWN_DURATION, 
     PlacementMode.DEFAULT); 
    </code> </td> 
   <td> N/D (automatico <span class="codeph"> CustomRange </span> modalità di segnalazione) </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> ManifestCue </span> Modalità di segnalazione </td> 
   <td> Non presente (annuncio disabilitato). </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;new&nbsp;Placement( 
     PlacementType.PRE_ROLL, 
     playhead, 
     Placement.UNKNOWN_DURATION, 
     PlacementMode.DEFAULT); 
    </code> </td> 
   <td> N/D (automatico <span class="codeph"> CustomRange </span> modalità di segnalazione) </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> CustomRange </span> Modalità di segnalazione </td> 
   <td> Non presente (annuncio disabilitato). </td> 
   <td> Nessuno </td> 
   <td> Nessuno (gestito in <span class="codeph"> CustomRangeOpportunityGenerator </span>) </td> 
  </tr> 
 </tbody> 
</table>
