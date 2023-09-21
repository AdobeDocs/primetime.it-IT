---
description: Queste classi forniscono informazioni sulla timeline di un particolare contenuto multimediale, incluso il posizionamento degli annunci.
title: Classi della sequenza temporale
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Classi della sequenza temporale{#timeline-classes}

Queste classi forniscono informazioni sulla timeline di un particolare contenuto multimediale, incluso il posizionamento degli annunci.

Pacchetto [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nome </th> 
   <th colname="2" class="entry"> <p>Descrizione </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/PlacementOpportunity.html" format="html" scope="external"> PlacementOpportunity</a></span> </td> 
   <td colname="2"> Una classe di opportunità rappresenta un punto di interesse sulla timeline. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> Timeline</a> </td> 
   <td colname="2"> Interfaccia che fornisce un iteratore per l'elaborazione dei marcatori timeline. Rappresenta la timeline del contenuto, comprese le interruzioni pubblicitarie. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> TimelineItem</a> </span> </td> 
   <td colname="2"> Classe. Rappresentazione immutabile generica di un elemento della timeline. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> IndicatoreTimeline</a> </span> </td> 
   <td colname="2"> Interfaccia che rappresenta un marcatore sulla timeline. Segna un'area di interesse sulla linea temporale effettiva. Attualmente, le aree di interesse sono gli annunci, che potresti voler contrassegnare, ad esempio, con un colore diverso nell’interfaccia utente della barra di scorrimento. Ogni marcatore è definito da una posizione e da una durata (ciascuna espressa in millisecondi). </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineOperation.html" format="html" scope="external"> OperazioneTimeline</a> </td> 
   <td colname="2"> Classe di base per tutte le operazioni che influiscono sulla sequenza temporale. </td> 
  </tr> 
 </tbody> 
</table>
