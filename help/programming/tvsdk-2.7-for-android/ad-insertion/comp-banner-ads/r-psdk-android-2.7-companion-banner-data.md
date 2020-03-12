---
description: Il contenuto di una AdAsset descrive un banner complementare.
seo-description: Il contenuto di una AdAsset descrive un banner complementare.
seo-title: Dati banner complementari
title: Dati banner complementari
uuid: 4a5d78e1-5abe-45a8-b50f-14f73fdcc879
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Dati banner complementari {#companion-banner-data}

Il contenuto di una AdAsset descrive un banner complementare.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Ciascuno `AdAsset` fornisce informazioni sulla visualizzazione della risorsa.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Informazioni disponibili </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> width </td> 
   <td colname="col2"> Larghezza del banner di accompagnamento, in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> Altezza del banner ausiliario, in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo di risorsa </td> 
   <td colname="col2">Il tipo di risorsa per il banner ausiliario: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: I dati si trovano nel codice HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: I dati sono un URL iframe (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL statico </td> 
   <td colname="col2"> <p>A volte, il banner ausiliario ha anche un <span class="codeph"> URL</span> statico che è un URL diretto per l’immagine o per un <span class="codeph"> .swf</span> (banner Flash). </p> <p>Se non desiderate utilizzare html o iframe, potete usare un URL diretto a un’immagine o un file SWF per visualizzare il banner nell’area di visualizzazione Flash. In questo caso, potete utilizzare <span class="codeph"> staticURL</span> per visualizzare il banner. </p> <p>Importante:  È necessario verificare se l'URL statico è una stringa valida, perché questa proprietà potrebbe non essere sempre disponibile. </p> </td> 
  </tr> 
 </tbody> 
</table>

