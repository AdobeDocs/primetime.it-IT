---
description: Il contenuto di un AdBannerAsset descrive un banner complementare.
seo-description: Il contenuto di un AdBannerAsset descrive un banner complementare.
seo-title: Dati banner complementari
title: Dati banner complementari
uuid: b2c709da-9d19-49d1-8116-9c947371b77c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Dati banner complementari{#companion-banner-data}

Il contenuto di un AdBannerAsset descrive un banner complementare.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

L&#39; `AdobePSDK.PSDKEventType.AD_STARTED` evento restituisce un&#39; `Ad` istanza che contiene una `companionAssets` proprietà ( `Array<AdBannerAsset>`).
Ciascuno `AdBannerAsset` fornisce informazioni sulla visualizzazione della risorsa.

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
     <li id="li_48E74AC5F00640EC8A4DE2CB31E106EC">static: I dati sono un URL immagine statico (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">
    <ph>
      dati banner
    </ph> </td> 
   <td colname="col2"> I dati del tipo specificato da <span class="codeph"> resourceType</span> per il banner ausiliario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL statico </td> 
   <td colname="col2"> <p>A volte il banner ausiliario può anche avere un URL statico che è un URL diretto all’immagine. </p> <p>Se non desiderate usare html o iframe, potete usare un URL diretto a un’immagine. In questo caso, potete utilizzare staticURL per visualizzare il banner. </p> <p>Importante:  È necessario verificare se l'URL statico è una stringa valida, perché questa proprietà potrebbe non essere sempre disponibile. </p> </td> 
  </tr> 
 </tbody> 
</table>

