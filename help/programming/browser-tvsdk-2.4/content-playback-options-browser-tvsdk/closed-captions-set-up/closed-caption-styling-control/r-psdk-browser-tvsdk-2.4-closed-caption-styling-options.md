---
description: È possibile specificare diverse opzioni di stile per i sottotitoli, che sostituiscono le opzioni di stile dei sottotitoli originali.
title: Opzioni di stile sottotitoli codificati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Opzioni di stile sottotitoli codificati{#closed-caption-styling-options}

È possibile specificare diverse opzioni di stile per i sottotitoli, che sostituiscono le opzioni di stile dei sottotitoli originali.

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
>Nelle opzioni che definiscono i valori predefiniti (ad esempio, `DEFAULT`), tale valore si riferisce all&#39;impostazione utilizzata quando la didascalia è stata originariamente specificata.

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
   <td colname="2"> <p>Tipo di carattere. </p> <p>Può essere impostato solo su un valore definito da <span class="codeph"> TextFormat.Font </span> e rappresenta, ad esempio, a spaziatura fissa con o senza servifs. </p> <p>Suggerimento: i tipi di carattere effettivi disponibili su un dispositivo possono variare e, se necessario, vengono utilizzate sostituzioni. Il monospazio con serifs è tipicamente usato come sostituto, anche se questa sostituzione può essere specifica per il sistema. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Dimensione </td> 
   <td colname="2"> <p>Dimensione della didascalia. </p> <p> Può essere impostato solo su un valore definito da <span class="codeph"> FormatoTesto.Dimensione </span> enumerazione: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIA </span> - Formato standard </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> GRANDE </span> - Circa il 30% più grande del medio </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> PICCOLO </span> - Circa il 30% più piccolo del medio </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> PREDEFINITO </span> : dimensione predefinita per la didascalia, uguale a media </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore font </td> 
   <td colname="2"> <p>Colore del carattere. </p> <p>Può essere impostato solo su un valore definito da <span class="codeph"> FormatoTesto.Colore </span> enumerazione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore di sfondo </td> 
   <td colname="2"> <p>Colore della cella del carattere di sfondo. </p> <p>Può essere impostato solo sui valori disponibili per il colore del carattere. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità font </td> 
   <td colname="2"> <p>Opacità del testo. </p> <p>Espresso in percentuale da 0 (completamente trasparente) a 100 (completamente opaco). <span class="codeph"> DEFAULT_OPACITY </span> il carattere è 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Interno inferiore </td> 
   <td colname="2"> <p>Distanza verticale dalla parte inferiore della finestra dei sottotitoli da evitare. </p> <p>Espresso come percentuale dell'altezza della finestra dei sottotitoli (ad esempio, "20%") o come numero di pixel (ad esempio, "20"). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Area utile </td> 
   <td colname="2"> <p>Area compresa tra 0% e 25% intorno al bordo dello schermo in cui i sottotitoli non verranno visualizzati. </p> <p>Per impostazione predefinita, l'area di sicurezza per 608/708 è 12% e l'area di sicurezza per WebVTT è 0%. Questa impostazione consente all'applicazione di ignorare tale impostazione predefinita. Se vengono forniti due valori, ad esempio la stringa "10%,20%", il primo valore è l’area di sicurezza orizzontale e il secondo valore è l’area di sicurezza verticale. Se viene fornito un valore, ad esempio la stringa "15%", sia l'asse verticale che l'asse orizzontale utilizzano l'area di sicurezza specificata. </p> </td> 
  </tr> 
 </tbody> 
</table>
