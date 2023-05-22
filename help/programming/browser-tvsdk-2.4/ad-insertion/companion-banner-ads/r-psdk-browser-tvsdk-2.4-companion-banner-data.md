---
description: Il contenuto di una risorsa AdBanner descrive un banner correlato.
title: Dati banner aziendale
exl-id: 94954233-4357-43be-a61f-6d8010c930ca
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Dati banner aziendale{#companion-banner-data}

Il contenuto di una risorsa AdBanner descrive un banner correlato.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Il `AdobePSDK.PSDKEventType.AD_STARTED` l&#39;evento restituisce un `Ad` istanza che contiene un `companionAssets` proprietà ( `Array<AdBannerAsset>`).
Ogni `AdBannerAsset` fornisce informazioni sulla visualizzazione della risorsa.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Informazioni disponibili </th> 
   <th colname="col2" class="entry"> Descrizione </th> 
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
     <li id="li_48E74AC5F00640EC8A4DE2CB31E106EC">statico: i dati sono un URL immagine statico (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">
    <pre>
      dati banner
    </pre> </td> 
   <td colname="col2"> Dati del tipo specificato da <span class="codeph"> resourceType</span> per questo banner. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL statico </td> 
   <td colname="col2"> <p>A volte il banner correlato può anche avere un URL statico che è un URL diretto all’immagine. </p> <p>Se non desideri utilizzare html o iframe, puoi utilizzare un URL diretto per un’immagine. In questo caso, puoi utilizzare staticURL per visualizzare il banner. </p> <p>Importante: è necessario verificare se l’URL statico è una stringa valida, perché questa proprietà potrebbe non essere sempre disponibile. </p> </td> 
  </tr> 
 </tbody> 
</table>
