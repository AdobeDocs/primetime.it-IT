---
description: È possibile specificare diverse opzioni di stile per le didascalie e queste opzioni sostituiscono le opzioni di stile nelle didascalie originali.
title: Opzioni per lo stile dei sottotitoli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Opzioni per lo stile dei sottotitoli{#closed-caption-styling-options}

È possibile specificare diverse opzioni di stile per le didascalie e queste opzioni sostituiscono le opzioni di stile nelle didascalie originali.

```js
new TextFormat( 
   font,  
   fontColor,  
   edgeColor,  
   fontEdge,  
   backgroundColor,  
   fillColor,  
   size,  
   fontOpacity,  
   backgroundOpacity,  
   fillOpacity, 
   bottomInset, 
   safeArea) 
```

>[!TIP]
>
>Nelle opzioni che definiscono i valori predefiniti (ad esempio, `DEFAULT`), tale valore si riferisce all’impostazione quando la didascalia è stata originariamente specificata.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Formato </th> 
   <th colname="2" class="entry"> Descrizione </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Font </td> 
   <td colname="2"> <p>Tipo di carattere. </p> <p>Può essere impostato solo su un valore definito dall'enumerazione <span class="codeph"> TextFormat.Font </span> e che rappresenta, ad esempio, la spaziatura con o senza serifs. </p> <p>Suggerimento:  I font effettivi disponibili su un dispositivo possono variare e vengono utilizzati sostituzioni quando necessario. Monospazio con i sieri viene generalmente utilizzato come sostituto, anche se questa sostituzione può essere specifica del sistema. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Dimensione </td> 
   <td colname="2"> <p>Dimensione della didascalia. </p> <p> Può essere impostato solo su un valore definito dall'enumerazione <span class="codeph"> TextFormat.Size </span> : 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIA  </span> - Dimensione standard </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> GRANDE  </span> - Circa il 30% più grande del medio </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> PICCOLO  </span> - Circa il 30% inferiore rispetto al medio </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> PREDEFINITO  </span> - Dimensione predefinita della didascalia; uguale al mezzo </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore font </td> 
   <td colname="2"> <p>Il colore del font. </p> <p>Può essere impostato solo su un valore definito dall'enumerazione <span class="codeph"> TextFormat.Color </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore di sfondo </td> 
   <td colname="2"> <p>Colore della cella del carattere di sfondo. </p> <p>Può essere impostato solo sui valori disponibili per il colore del font. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> opacità del carattere </td> 
   <td colname="2"> <p>opacità del testo. </p> <p>Espresso in percentuale da 0 (completamente trasparente) a 100 (completamente opaco). <span class="codeph"> DEFAULT_OPACITY  </span> per il font è 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Ingresso inferiore </td> 
   <td colname="2"> <p>Distanza verticale dalla parte inferiore della finestra della didascalia per evitare didascalie. </p> <p>Espresso come percentuale dell’altezza della finestra della didascalia (ad esempio, "20%") o come numero di pixel (ad esempio, "20"). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Area di sicurezza </td> 
   <td colname="2"> <p>Area intorno al bordo dello schermo compresa tra 0% e 25% in cui i sottotitoli non verranno visualizzati. </p> <p>Per impostazione predefinita, l’area di sicurezza per 608/708 è del 12% e l’area di sicurezza per WebVTT è dello 0%. Questa impostazione consente all’applicazione di ignorare tale impostazione predefinita. Se vengono forniti due valori, ad esempio la stringa "10%,20%", il primo valore è l'area di sicurezza orizzontale e il secondo valore è l'area di sicurezza verticale. Se viene fornito un valore, ad esempio la stringa "15%", sia gli assi verticali che orizzontali utilizzano l'area di sicurezza specificata. </p> </td> 
  </tr> 
 </tbody> 
</table>

