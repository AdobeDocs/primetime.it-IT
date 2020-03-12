---
description: È possibile specificare diverse opzioni di stile delle didascalie, che sostituiscono le opzioni di stile nelle didascalie originali.
seo-description: È possibile specificare diverse opzioni di stile delle didascalie, che sostituiscono le opzioni di stile nelle didascalie originali.
seo-title: Opzioni di stile dei sottotitoli codificati
title: Opzioni di stile dei sottotitoli codificati
uuid: 0e2fd9f3-e569-4b5d-9b78-86f8ee6230ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Opzioni di stile dei sottotitoli codificati{#closed-caption-styling-options}

È possibile specificare diverse opzioni di stile delle didascalie, che sostituiscono le opzioni di stile nelle didascalie originali.

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
>Nelle opzioni che definiscono i valori predefiniti (ad esempio, `DEFAULT`), tale valore si riferisce a ciò che era l&#39;impostazione quando la didascalia era originariamente specificata.

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
   <td colname="2"> <p>Il tipo di carattere. </p> <p>Può essere impostato solo su un valore definito dall'enumerazione <span class="codeph"> TextFormat.Font </span> e rappresenta, ad esempio, una spaziatura con o senza serifi. </p> <p>Suggerimento:  I font effettivamente disponibili su un dispositivo possono variare e, se necessario, vengono utilizzate delle sostituzioni. Il monospazio con i serifi viene in genere utilizzato come sostituto, anche se questa sostituzione può essere specifica del sistema. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Dimensioni </td> 
   <td colname="2"> <p>Dimensione della didascalia. </p> <p> Può essere impostato solo su un valore definito dall'enumerazione <span class="codeph"> TextFormat.Size </span> : 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIUM </span> - Dimensione standard </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> GRANDE </span> - Circa il 30% più grande del medio </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> PICCOLO </span> - Circa il 30% inferiore a medio </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> PREDEFINITO </span> - La dimensione predefinita della didascalia; come media </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore font </td> 
   <td colname="2"> <p>Il colore del font. </p> <p>Può essere impostato solo su un valore definito dall'enumerazione <span class="codeph"> TextFormat.Color </span> . </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore di sfondo </td> 
   <td colname="2"> <p>Colore della cella del carattere di sfondo. </p> <p>Può essere impostato solo su valori disponibili per il colore del font. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità del font </td> 
   <td colname="2"> <p>Opacità del testo. </p> <p>Espressa come percentuale da 0 (completamente trasparente) a 100 (completamente opaca). <span class="codeph"> DEFAULT_OPACITY </span> per il font è 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Ingresso inferiore </td> 
   <td colname="2"> <p>Distanza verticale dalla parte inferiore della finestra della didascalia per evitare la comparsa di didascalie. </p> <p>Espressa come percentuale dell'altezza della finestra della didascalia (ad esempio, "20%") o come numero di pixel (ad esempio, "20"). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Area di sicurezza </td> 
   <td colname="2"> <p>Un'area intorno al bordo dello schermo compresa tra 0% e 25% in cui le didascalie non verranno visualizzate. </p> <p>Per impostazione predefinita, l'area di sicurezza per 608/708 è 12% e l'area di sicurezza per WebVTT è 0%. Questa impostazione consente all'applicazione di ignorare tale impostazione predefinita. Se vengono forniti due valori, ad esempio la stringa "10%,20%", il primo valore è l'area di sicurezza orizzontale e il secondo valore è l'area di sicurezza verticale. Se viene fornito un valore, ad esempio la stringa "15%", sia gli assi verticali che orizzontali utilizzano l'area di sicurezza specificata. </p> </td> 
  </tr> 
 </tbody> 
</table>

