---
description: Il contenuto di un AdBannerAsset descrive un banner correlato.
title: Dati banner Companion
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Dati banner Companion{#companion-banner-data}

Il contenuto di un AdBannerAsset descrive un banner correlato.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

L&#39;evento `AdobePSDK.PSDKEventType.AD_STARTED` restituisce un&#39;istanza `Ad` che contiene una proprietà `companionAssets` ( `Array<AdBannerAsset>`).
Ogni elemento `AdBannerAsset` fornisce informazioni sulla visualizzazione della risorsa.

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
   <td colname="col2"> Larghezza del banner correlato in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> altezza </td> 
   <td colname="col2"> Altezza del banner correlato in pixel. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo di risorsa </td> 
   <td colname="col2">Tipo di risorsa per il banner correlato: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html I dati sono nel codice HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: I dati sono un URL iframe (src). </li> 
     <li id="li_48E74AC5F00640EC8A4DE2CB31E106EC">statico: I dati sono un URL immagine statico (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">
    <pre>
      dati banner
    </pre> </td> 
   <td colname="col2"> I dati del tipo specificato da <span class="codeph"> resourceType</span> per questo banner correlato. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL statico </td> 
   <td colname="col2"> <p>A volte il banner correlato potrebbe avere anche un URL statico che è un URL diretto all’immagine. </p> <p>Se non desideri utilizzare html o iframe, puoi utilizzare un URL diretto a un’immagine. In questo caso, puoi utilizzare staticURL per visualizzare il banner. </p> <p>Importante:  È necessario verificare se l’URL statico è una stringa valida, perché questa proprietà potrebbe non essere sempre disponibile. </p> </td> 
  </tr> 
 </tbody> 
</table>

