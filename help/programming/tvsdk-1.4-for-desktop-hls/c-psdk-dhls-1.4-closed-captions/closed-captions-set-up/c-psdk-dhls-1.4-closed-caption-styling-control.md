---
description: È possibile fornire informazioni sullo stile per i brani con sottotitoli codificati utilizzando la classe ClosedCaptionStyles. Imposta lo stile per i sottotitoli che vengono visualizzati dal lettore.
title: Controlla lo stile dei sottotitoli
exl-id: fd94a851-1e8f-4406-a3bb-ca115b4e60f8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Controlla lo stile dei sottotitoli{#control-closed-caption-styling}

È possibile fornire informazioni sullo stile per i brani con sottotitoli codificati utilizzando la classe ClosedCaptionStyles. Imposta lo stile per i sottotitoli che vengono visualizzati dal lettore.

Questa classe racchiude informazioni sullo stile dei sottotitoli codificati, ad esempio il tipo di carattere, la dimensione, il colore e l&#39;opacità dello sfondo. Una classe helper associata, `ClosedCaptionStylesBuilder`, facilita l&#39;utilizzo delle impostazioni di stile sottotitoli.

## Imposta stili sottotitoli codificati {#section_DAE84659D1964DB1B518F91B59AF29D9}

È possibile applicare uno stile al testo con sottotitoli codificati con i metodi TVSDK.

1. Attendere che MediaPlayer abbia almeno lo stato READY (vedere [Attesa di uno stato valido](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)).
1. Per modificare le impostazioni di stile, effettuate una delle seguenti operazioni:

   * Utilizza il `ClosedCaptionStylesBuilder` classe helper (funziona su `ClosedCaptionStyles` dietro le quinte).
   * Utilizza il `ClosedCaptionStyles` direttamente in classe.

>[!NOTE]
>
>L&#39;impostazione dello stile dei sottotitoli è un&#39;operazione asincrona e potrebbe richiedere alcuni secondi prima che le modifiche vengano visualizzate sullo schermo.

## Opzioni di stile sottotitoli codificati {#section_D28F50B98C0D48CF89C4FB6DC81C5185}

È possibile fornire informazioni sullo stile delle tracce di sottotitoli codificati utilizzando `ClosedCaptionStyles` classe. Imposta lo stile per i sottotitoli che vengono visualizzati dal lettore.

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
   <td colname="2"> <p>Tipo di carattere. </p> <p>Può essere impostato solo su un valore definito da <span class="codeph"> ClosedCaptionStyles.FONT </span> e rappresenta, ad esempio, a spaziatura fissa con o senza serif. 
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
     </code> </p> <p>Suggerimento: i tipi di carattere effettivi disponibili su un dispositivo possono variare e, se necessario, vengono utilizzate sostituzioni. Il monospazio con serifs è tipicamente usato come sostituto, anche se questa sostituzione può essere specifica per il sistema. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Dimensione </td> 
   <td colname="2"> <p>Dimensione della didascalia. </p> <p> Può essere impostato solo su un valore definito da <span class="codeph"> ClosedCaptionStyles.FONT_SIZE </span> array: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIA </span> - Formato standard </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> GRANDE </span> - Circa il 30% più grande del medio </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> PICCOLO </span> - Circa il 30% più piccolo del medio </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> PREDEFINITO </span> : dimensione predefinita per la didascalia, uguale a media </li> 
     </ul> </p> <p>Suggerimento: è possibile modificare la dimensione del carattere dei sottotitoli WebVTT modificando il parametro di dimensione per <span class="codeph"> Impostazione DefaultMediaPlayer.ccStyles </span> funzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Bordo font </td> 
   <td colname="2"> <p>Effetto utilizzato per il bordo del font, ad esempio in rilievo o nessuno. </p> <p>Può essere impostato solo su un valore definito da <span class="codeph"> ClosedCaptionStyles.FONT_EDGE </span> array. 
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
   <td colname="2"> <p>Colore del carattere. </p> <p>Può essere impostato solo su un valore definito da <span class="codeph"> ClosedCaptionStyles.COLOR </span> array. 
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
   <td colname="2"> <p>Colore dell'effetto bordo. </p> <p>Può essere impostato su uno qualsiasi dei valori disponibili per il colore del carattere. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore di sfondo </td> 
   <td colname="2"> <p>Colore della cella del carattere di sfondo. </p> <p>Può essere impostato solo sui valori disponibili per il colore del carattere. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore riempimento </td> 
   <td colname="2"> <p>Colore dello sfondo della finestra in cui si trova il testo. </p> <p>Può essere impostato su uno qualsiasi dei valori disponibili per il colore del carattere. </p> <p>Importante: questo non si applica ai sottotitoli WebVTT, perché WebVTT non utilizza questa funzione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità font </td> 
   <td colname="2"> <p>Opacità del testo. </p> <p>Espresso in percentuale da 0 (completamente trasparente) a 100 (completamente opaco). <span class="codeph"> DEFAULT_OPACITY </span> il carattere è 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità sfondo </td> 
   <td colname="2"> <p>Opacità della cella del carattere di sfondo. </p> <p>Espresso in percentuale da 0 (completamente trasparente) a 100 (completamente opaco). <span class="codeph"> DEFAULT_OPACITY </span> per lo sfondo è 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità riempimento </td> 
   <td colname="2"> <p>Opacità dello sfondo della finestra della didascalia. </p> <p>Espresso in percentuale da 0 (completamente trasparente) a 100 (completamente opaco). <span class="codeph"> DEFAULT_OPACITY </span> per il riempimento è 0. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Esempi: Formattazione dei sottotitoli {#section_63E33840B7A14D26990046E2ACF2ECA1}

È possibile specificare la formattazione dei sottotitoli.

## Esempio 1: specificare esplicitamente i valori di formato {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

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

## Esempio 2: specificare i valori di formato nei parametri {#section_147036D7C31C4010A5A7DF49997014A9}

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
