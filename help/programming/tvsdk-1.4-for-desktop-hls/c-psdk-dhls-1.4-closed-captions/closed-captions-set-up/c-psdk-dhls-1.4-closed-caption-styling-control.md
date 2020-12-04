---
description: Potete fornire informazioni sullo stile per le tracce di sottotitoli codificati utilizzando la classe ClosedCaptionStyles. Questo imposta lo stile per tutte le didascalie visualizzate dal lettore.
seo-description: Potete fornire informazioni sullo stile per le tracce di sottotitoli codificati utilizzando la classe ClosedCaptionStyles. Questo imposta lo stile per tutte le didascalie visualizzate dal lettore.
seo-title: Controllo dello stile dei sottotitoli codificati
title: Controllo dello stile dei sottotitoli codificati
uuid: 506c06d3-8fe0-46c9-9ed6-5b35d21c021c
translation-type: tm+mt
source-git-commit: b67a9dcb0abb07f4fdff4e03d9d6c0b07ff45127
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---


# Controllo dello stile dei sottotitoli codificati{#control-closed-caption-styling}

Potete fornire informazioni sullo stile per le tracce di sottotitoli codificati utilizzando la classe ClosedCaptionStyles. Questo imposta lo stile per tutte le didascalie visualizzate dal lettore.

Questa classe racchiude informazioni sullo stile dei sottotitoli codificati quali tipo di font, dimensione, colore e opacità dello sfondo. Una classe helper associata, `ClosedCaptionStylesBuilder`, facilita l&#39;utilizzo delle impostazioni di stile dei sottotitoli codificati.

## Impostare gli stili di sottotitoli codificati {#section_DAE84659D1964DB1B518F91B59AF29D9}

Potete formattare il testo dei sottotitoli codificati con i metodi TVSDK.

1. Attendete che MediaPlayer disponga almeno dello stato PREPARATO (vedere [Attendere uno stato valido](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)).
1. Per modificare le impostazioni di stile, effettuate una delle seguenti operazioni:

   * Utilizzate la classe helper `ClosedCaptionStylesBuilder` (che funziona su `ClosedCaptionStyles` dietro le quinte).
   * Utilizzate direttamente la classe `ClosedCaptionStyles`.

>[!NOTE]
>
>L&#39;impostazione dello stile dei sottotitoli codificati è un&#39;operazione asincrona, pertanto la visualizzazione delle modifiche sullo schermo potrebbe richiedere alcuni secondi.

## Opzioni di stile dei sottotitoli codificati {#section_D28F50B98C0D48CF89C4FB6DC81C5185}

Potete fornire informazioni sullo stile per le tracce di sottotitoli codificati utilizzando la classe `ClosedCaptionStyles`. Questo imposta lo stile per tutte le didascalie visualizzate dal lettore.

```
public function TextFormat( 
   font:String = default,  
   size:String = default,  
   fontEdge:String = default,  
   fontColor:String = default,  
   backgroundColor:String = default,  
   fillColor:String = default,  
   edgeColor:String = default,  
   fontOpacity:int,  
   backgroundOpacity:int,  
   fillOpacity:int)
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
   <td colname="2"> <p>Il tipo di carattere. </p> <p>Può essere impostato solo su un valore definito dall'array <span class="codeph"> ClosedCaptionStyles.FONT </span> e rappresenta, ad esempio, una spaziatura con o senza serifi. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;AVCaptionStyle.MONOSPACE_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.MONOSPACED_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.CASUAL, 
      &nbsp;AVCaptionStyle.CURSIVE, 
      &nbsp;AVCaptionStyle.SMALL_CAPITALS 
      &nbsp;]; 
     </code> </p> <p>Suggerimento:  I font effettivamente disponibili su un dispositivo possono variare e, se necessario, vengono utilizzate delle sostituzioni. Il monospazio con i serifi viene in genere utilizzato come sostituto, anche se questa sostituzione può essere specifica del sistema. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Dimensioni </td> 
   <td colname="2"> <p>Dimensione della didascalia. </p> <p> È possibile impostare solo un valore definito dall'array <span class="codeph"> ClosedCaptionStyles.FONT_SIZE </span>: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIUM  </span> - Dimensione standard </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> GRANDE  </span> - Circa il 30% più grande del medio </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> PICCOLA  </span> - Circa il 30% inferiore al medio </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> PREDEFINITO  </span> - La dimensione predefinita della didascalia; come media </li> 
     </ul> </p> <p>Suggerimento:  È possibile modificare la dimensione del font delle didascalie WebVTT modificando il parametro della dimensione per la funzione <span class="codeph"> DefaultMediaPlayer.ccStyles setter </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Bordo font </td> 
   <td colname="2"> <p>Effetto usato per il bordo del font, ad esempio sollevato o nessuno. </p> <p>Può essere impostato solo su un valore definito dall'array <span class="codeph"> ClosedCaptionStyles.FONT_EDGE </span>. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT_EDGE&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.NONE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RAISED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEPRESSED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.UNIFORM, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.LEFT_DROP_SHADOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RIGHT_DROP_SHADOW 
      &nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore font </td> 
   <td colname="2"> <p>Il colore del font. </p> <p>Può essere impostato solo su un valore definito dall'array <span class="codeph"> ClosedCaptionStyles.COLOR </span>. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;COLOR&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLACK, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GRAY, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_CYAN&nbsp;&nbsp;&nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore bordo </td> 
   <td colname="2"> <p>Colore dell’effetto bordo. </p> <p>Può essere impostato su uno qualsiasi dei valori disponibili per il colore del font. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore di sfondo </td> 
   <td colname="2"> <p>Colore della cella del carattere di sfondo. </p> <p>Può essere impostato solo su valori disponibili per il colore del font. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore riempimento </td> 
   <td colname="2"> <p>Colore dello sfondo della finestra in cui si trova il testo. </p> <p>Può essere impostato su uno qualsiasi dei valori disponibili per il colore del font. </p> <p>Importante:  Ciò non si applica alle didascalie WebVTT, perché WebVTT non utilizza questa funzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità del font </td> 
   <td colname="2"> <p>Opacità del testo. </p> <p>Espressa come percentuale da 0 (completamente trasparente) a 100 (completamente opaca). <span class="codeph"> DEFAULT_OPACITY  </span> per il font è 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità di sfondo </td> 
   <td colname="2"> <p>Opacità della cella del carattere di sfondo. </p> <p>Espressa come percentuale da 0 (completamente trasparente) a 100 (completamente opaca). <span class="codeph"> DEFAULT_OPACITY  </span> per lo sfondo è 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità riempimento </td> 
   <td colname="2"> <p>Opacità dello sfondo della finestra della didascalia. </p> <p>Espressa come percentuale da 0 (completamente trasparente) a 100 (completamente opaca). <span class="codeph"> DEFAULT_OPACITY  </span> per il riempimento è 0. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Esempi: Formattazione didascalia {#section_63E33840B7A14D26990046E2ACF2ECA1}

È possibile specificare la formattazione dei sottotitoli codificati.

## Esempio 1: Specificare i valori di formato in modo esplicito {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

```
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    var formatBuilder:TextFormatBuilder = new TextFormatBuilder(); 
    formatBuilder.font = Font.DEFAULT,  
    formatBuilder.fontSize = FontSize.DEFAULT,  
    formatBuilder.fontEdge = FontEdge.DEFAULT,  
    formatBuilder.fontColor = Color.DEFAULT,  
    formatBuilder.backgroundColor = Color.DEFAULT,  
    formatBuilder.fillColor = Color.DEFAULT,  
    formatBuilder.edgeColor = Color.DEFAULT,  
    formatBuilder.fontOpacity = .DEFAULT_OPACITY,  
    formatBuilder.backgroundOpacity = Font.DEFAULT_OPACITY,  
    formatBuilder.fillOpacity = TextFormat.DEFAULT_OPACITY 
    mediaPlayer.set CCStyle(formatBuilder.toTextFormat()); 
} 
```

## Esempio 2: Specificare i valori di formato nei parametri {#section_147036D7C31C4010A5A7DF49997014A9}

```
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param fontSize 
* The desired text size. 
* @param fontEdge 
* The desired font edge. 
* @param fontColor 
* The desired font color. 
* @param backgroundColor 
* The desired background color. 
* @param fillColor 
* The desired fill color. 
* @param edgeColor 
* The desired color to draw the text edges. 
* @param fontOpacity 
* The desired font opacity. 
* @param backgroundOpacity 
* The desired background opacity. 
* @param fillOpacity 
* The desired fill opacity. 
*/ 
public function TextFormatBuilder(font:Font, fontSize:FontSize, fontEdge:FontEdge,  
                                  fontColor:Color, backgroundColor:Color,  
                                  fillColor:Color, edgeColor:Color, fontOpacity:int, 
                                  backgroundOpacity:int, fillOpacity:int); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public function toTextFormat():TextFormat; 
... 
```
