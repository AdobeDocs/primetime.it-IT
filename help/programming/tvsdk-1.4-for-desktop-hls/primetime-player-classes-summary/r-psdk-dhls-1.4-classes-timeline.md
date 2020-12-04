---
description: Queste classi forniscono informazioni sulla cronologia dei supporti specifici, inclusa la posizione degli annunci.
seo-description: Queste classi forniscono informazioni sulla cronologia dei supporti specifici, inclusa la posizione degli annunci.
seo-title: Classi Timeline
title: Classi Timeline
uuid: 9c06fec1-d725-4fe8-9cf5-1e3ade2b7d27
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 0%

---


# Classi Timeline{#timeline-classes}

Queste classi forniscono informazioni sulla cronologia dei supporti specifici, inclusa la posizione degli annunci.

Pacchetto: [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nome </th> 
   <th colname="2" class="entry"> <p>Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> ContentTracker  </a> </span> </td> 
   <td colname="2"> Interfaccia che definisce il protocollo da implementare se si desidera creare un modulo di tracciamento del contenuto progettato per l’integrazione con la libreria TVSDK. <p>Per questa interfaccia è necessario definire il modo in cui gli eventi di avanzamento vengono segnalati al sistema di tracciamento remoto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> Opportunità  </a> </span> </td> 
   <td colname="2"> Classe di base per tutte le classi di opportunità. Una classe di opportunità rappresenta un punto "interessante" sulla timeline. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> Posizionamento  </a> </span> </td> 
   <td colname="2"> Classe che racchiude informazioni relative alla posizione della timeline. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> PlacementMode  </a> </span> </td> 
   <td colname="2"> Enumerazione delle modalità di posizionamento, ad esempio se inserire o sostituire il contenuto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> PlacementType  </a> </span> </td> 
   <td colname="2"> enumerazione di tipi di posizionamento che indicano la posizione nella timeline; ad esempio, PRE_ROLL. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> Prenotazione  </a> </span> </td> 
   <td colname="2"> Una prenotazione viene utilizzata per limitare o impedire l'ulteriore elaborazione di un determinato intervallo di tempo sulla timeline. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> Timeline  </a> </span> </td> 
   <td colname="2"> Interfaccia che fornisce un iteratore per l’elaborazione dei marcatori timeline. Rappresenta la timeline del contenuto, comprese le interruzioni di annuncio. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> TimelineItem  </a> </span> </td> 
   <td colname="2"> Classe. Rappresentazione immutabile generica di un elemento della cronologia. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> TimelineMarker  </a> </span> </td> 
   <td colname="2"> Classe che rappresenta un marcatore sulla timeline. Indica un'area di interesse sulla timeline effettiva. Attualmente, le aree di interesse sono gli annunci, che potresti voler contrassegnare, ad esempio, con un colore diverso nell’interfaccia della barra di scorrimento. Ciascun indicatore è definito da una posizione e una durata (ciascuna espressa in millisecondi). </td> 
  </tr> 
 </tbody> 
</table>

