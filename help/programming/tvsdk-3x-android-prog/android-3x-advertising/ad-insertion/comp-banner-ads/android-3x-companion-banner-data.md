---
description: Il contenuto di un AdAsset descrive un banner correlato.
title: Dati banner aziendale
exl-id: fae96cb8-0092-43ed-a26b-cdaa1389a368
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# Dati banner aziendale {#companion-banner-data}

Il contenuto di un AdAsset descrive un banner correlato.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Ogni `AdAsset` fornisce informazioni sulla visualizzazione della risorsa.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Informazioni disponibili </b></th> 
   <th colname="col2" class="entry"> <b>Descrizione</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> larghezza </td> 
   <td colname="col2"> Larghezza in pixel del banner correlato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> altezza </td> 
   <td colname="col2"> Altezza del banner correlato in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo di risorsa </td> 
   <td colname="col2">Il tipo di risorsa per questo banner correlato: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: i dati sono nel codice HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: i dati sono un URL iframe (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL statico </td> 
   <td colname="col2"> <p>A volte, il banner correlato presenta anche un <span class="codeph"> staticURL</span> che è un URL diretto all’immagine o a un <span class="codeph"> .swf</span> (banner flash). </p> <p>Se non desideri utilizzare html o iframe, puoi utilizzare un URL diretto per un’immagine o un file swf per visualizzare il banner nella fase di Flash. In questo caso, puoi utilizzare <span class="codeph"> staticURL</span> per visualizzare il banner. </p> <p>Importante: è necessario verificare se l’URL statico è una stringa valida, perché questa proprietà potrebbe non essere sempre disponibile. </p> </td> 
  </tr> 
 </tbody> 
</table>
