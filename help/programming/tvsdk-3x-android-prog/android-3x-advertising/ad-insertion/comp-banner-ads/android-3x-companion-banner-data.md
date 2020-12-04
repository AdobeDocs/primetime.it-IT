---
description: Il contenuto di una AdAsset descrive un banner complementare.
seo-description: Il contenuto di una AdAsset descrive un banner complementare.
seo-title: Dati banner complementari
title: Dati banner complementari
uuid: f54aecea-5e11-45dd-97d0-5774ca631a4d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Dati del banner della compagnia {#companion-banner-data}

Il contenuto di una AdAsset descrive un banner complementare.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Ogni `AdAsset` fornisce informazioni sulla visualizzazione della risorsa.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Informazioni disponibili  </b></th> 
   <th colname="col2" class="entry"> <b>Descrizione</b> </th> 
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
   <td colname="col2"> <p>A volte, il banner ausiliario ha anche un <span class="codeph"> staticURL</span> che è un URL diretto per l'immagine o per un <span class="codeph"> .swf</span> (banner Flash). </p> <p>Se non desiderate utilizzare html o iframe, potete utilizzare un URL diretto a un’immagine o un file SWF per visualizzare invece il banner nell’area di visualizzazione dell’Flash. In questo caso, potete utilizzare <span class="codeph"> staticURL</span> per visualizzare il banner. </p> <p>Importante:  È necessario verificare se l'URL statico è una stringa valida, perché questa proprietà potrebbe non essere sempre disponibile. </p> </td> 
  </tr> 
 </tbody> 
</table>