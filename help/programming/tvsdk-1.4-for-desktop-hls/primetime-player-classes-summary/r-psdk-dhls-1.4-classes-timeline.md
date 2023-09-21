---
description: Queste classi forniscono informazioni sulla timeline di un particolare contenuto multimediale, incluso il posizionamento degli annunci.
title: Classi della sequenza temporale
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Classi della sequenza temporale{#timeline-classes}

Queste classi forniscono informazioni sulla timeline di un particolare contenuto multimediale, incluso il posizionamento degli annunci.

Pacchetto [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nome </th> 
   <th colname="2" class="entry"> <p>Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> ContentTracker </a> </span> </td> 
   <td colname="2"> Interfaccia che definisce il protocollo da implementare per creare un modulo di tracciamento dei contenuti progettato per l’integrazione con la libreria TVSDK. <p>Questa interfaccia richiede la definizione del modo in cui gli eventi di avanzamento vengono segnalati al sistema di tracciamento remoto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> opportunità </a> </span> </td> 
   <td colname="2"> Classe base per tutte le classi di opportunità. Una classe di opportunità rappresenta un punto "interessante" sulla timeline. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> Posizione </a> </span> </td> 
   <td colname="2"> Classe che racchiude le informazioni relative al posizionamento della timeline. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> PlacementMode </a> </span> </td> 
   <td colname="2"> Enumerazione delle modalità di posizionamento, ad esempio se inserire o sostituire il contenuto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> PlacementType </a> </span> </td> 
   <td colname="2"> Enumerazione dei tipi di posizionamento che indicano dove viene effettuato il posizionamento nella timeline, ad esempio PRE_ROLL. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> Prenotazione </a> </span> </td> 
   <td colname="2"> Una prenotazione viene utilizzata per limitare o impedire l’ulteriore elaborazione di un determinato intervallo di tempo sulla timeline. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> Timeline </a> </span> </td> 
   <td colname="2"> Interfaccia che fornisce un iteratore per l'elaborazione dei marcatori timeline. Rappresenta la timeline del contenuto, comprese le interruzioni pubblicitarie. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> TimelineItem </a> </span> </td> 
   <td colname="2"> Classe. Rappresentazione immutabile generica di un elemento della timeline. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> IndicatoreTimeline </a> </span> </td> 
   <td colname="2"> Classe che rappresenta un marcatore sulla timeline. Segna un'area di interesse sulla linea temporale effettiva. Attualmente, le aree di interesse sono gli annunci, che potresti voler contrassegnare, ad esempio, con un colore diverso nell’interfaccia utente della barra di scorrimento. Ogni marcatore è definito da una posizione e da una durata (ciascuna espressa in millisecondi). </td> 
  </tr> 
 </tbody> 
</table>
