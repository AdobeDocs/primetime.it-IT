---
description: È possibile fornire informazioni sullo stile per le tracce di sottotitoli codificati utilizzando la classe TextFormat. Questo imposta lo stile per tutte le didascalie visualizzate dal lettore.
seo-description: È possibile fornire informazioni sullo stile per le tracce di sottotitoli codificati utilizzando la classe TextFormat. Questo imposta lo stile per tutte le didascalie visualizzate dal lettore.
seo-title: Controllo dello stile dei sottotitoli codificati
title: Controllo dello stile dei sottotitoli codificati
uuid: 331b0833-3e8a-482e-a3df-5e92b69d0a94
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Controllo dello stile dei sottotitoli codificati {#control-closed-caption-styling-overview}

È possibile fornire informazioni sullo stile per le tracce di sottotitoli codificati utilizzando la classe TextFormat. Questo imposta lo stile per tutte le didascalie visualizzate dal lettore.

Questa classe racchiude informazioni sullo stile dei sottotitoli codificati quali tipo di font, dimensione, colore e opacità dello sfondo. Una classe helper associata `TextFormatBuilder`facilita l&#39;utilizzo delle impostazioni di stile dei sottotitoli codificati.

## Impostare gli stili di didascalia {#set-closed-caption-styles}

Potete formattare il testo dei sottotitoli codificati con i metodi TVSDK.

1. Attendete che il lettore multimediale sia almeno nello stato PREPARATO.
1. Create un&#39; `TextFormatBuilder` istanza.

   Potete fornire ora tutti i parametri di stile per i sottotitoli codificati o impostarli successivamente.

   TVSDK racchiude informazioni sullo stile dei sottotitoli codificati nell&#39; `TextFormat` interfaccia. La `TextFormatBuilder` classe crea oggetti che implementano questa interfaccia.

   ```java
   public TextFormatBuilder( 
      Font font, 
      Size size, 
      FontEdge fontEdge, 
      Color fontColor, 
      Color backgroundColor, 
      Color fillColor, 
      Color edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity)
   ```

1. Per ottenere un riferimento a un oggetto che implementa l&#39; `TextFormat` interfaccia, chiamare il metodo `TextFormatBuilder.toTextFormat` public.

   Questo restituisce un `TextFormat` oggetto che può essere applicato al lettore multimediale.

   ```java
   public TextFormat toTextFormat()
   ```

1. Facoltativamente, per ottenere le impostazioni correnti per lo stile dei sottotitoli codificati, effettuate una delle seguenti operazioni:

   * Ottenete tutte le impostazioni di stile con `MediaPlayer.getCCStyle`.

      Il valore restituito è un&#39;istanza dell&#39; `TextFormat` interfaccia.

      ```js
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws IllegalStateException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws IllegalStateException;
      ```

   * Ottenete le impostazioni una alla volta tramite i metodi `TextFormat` getter dell&#39;interfaccia.

      ```js
      public Color getFontColor(); 
      public Color getBackgroundColor(); 
      public Color getFillColor(); // retrieve the font fill color 
      public Color getEdgeColor(); // retrieve the font edge color 
      public Size getSize(); // retrieve the font size 
      public FontEdge getFontEdge(); // retrieve the font edge type 
      public Font getFont(); // retrieve the font type 
      public int getFontOpacity(); 
      public int getBackgroundOpacity();
      ```

1. Per modificare le impostazioni di stile, effettuare una delle seguenti operazioni:

   >[!NOTE]
   >
   >Non è possibile modificare la dimensione delle didascalie WebVTT.

   * Utilizzate il metodo setter `MediaPlayer.setCCStyle`, passando un&#39;istanza dell&#39; `TextFormat` interfaccia:

      ```js
      /** 
      * Sets the closed captioning style. Used to control the closed captioning font, 
      * size, color, edge and opacity.  
      * 
      * This method is safe to use even if the current media stream doesn't have closed 
      * captions. 
      * 
      * @param textFormat 
      * @throws IllegalStateException 
      */ 
      public void setCCStyle(TextFormat textFormat) throws IllegalStateException;
      ```

   * Utilizzare la `TextFormatBuilder` classe, che definisce i singoli metodi setter.

      L&#39; `TextFormat` interfaccia definisce un oggetto immutabile, quindi esistono solo metodi getter e nessun setter. È possibile impostare i parametri di stile dei sottotitoli codificati solo con la `TextFormatBuilder` classe:

      ```js
      // set font type 
      public void setFont(Font font)  
      public void setBackgroundColor(Color backgroundColor) 
      public void setFillColor(Color fillColor) 
      // set the font-edge color 
      public void setEdgeColor(Color edgeColor)  
      // set the font size 
      public void setSize(Size size)  
      // set the font edge type 
      public void setFontEdge(FontEdge fontEdge)  
      public void setFontOpacity(int fontOpacity) 
      public void setBackgroundOpacity(int backgroundOpacity) 
      // set the font-fill opacity level 
      public void setFillOpacity(int fillOpacity)  
      public void setFontColor(Color fontColor)
      ```

L&#39;impostazione dello stile dei sottotitoli codificati è un&#39;operazione asincrona, pertanto la visualizzazione delle modifiche sullo schermo potrebbe richiedere alcuni secondi.

## Opzioni di stile dei sottotitoli codificati {#closed-caption-styling-options}

È possibile specificare diverse opzioni di stile delle didascalie, che sostituiscono le opzioni di stile nelle didascalie originali

```
public TextFormatBuilder(
 Font font,
 Size size,
 FontEdge fontEdge,
 Color fontColor,
 Color backgroundColor,
 Color fillColor,
 Color edgeColor,
 int fontOpacity,
 int backgroundOpacity,
 int fillOpacity,
 String bottomInset)
```

[!TIP]
Nelle opzioni che definiscono i valori predefiniti (ad esempio, PREDEFINITO), tale valore si riferisce a ciò che era l&#39;impostazione quando la didascalia era originariamente specificata.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> Formato </b></th> 
   <th colname="2" class="entry"> <b>Descrizione</b> </th> 
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
   <td colname="1"> Bordo font </td> 
   <td colname="2"> <p>Effetto usato per il bordo del font, ad esempio sollevato o nessuno. </p> <p>Può essere impostato solo su un valore definito dall'enumerazione <span class="codeph"> TextFormat.FontEdge </span> . </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore font </td> 
   <td colname="2"> <p>Il colore del font. </p> <p>Può essere impostato solo su un valore definito dall'enumerazione <span class="codeph"> TextFormat.Color </span> . </p> </td> 
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
   <td colname="2"> <p>Colore dello sfondo della finestra in cui si trova il testo. </p> <p>Può essere impostato su uno qualsiasi dei valori disponibili per il colore del font. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità del font </td> 
   <td colname="2"> <p>Opacità del testo. </p> <p>Espressa come percentuale da 0 (completamente trasparente) a 100 (completamente opaca). <span class="codeph"> DEFAULT_OPACITY </span> per il font è 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità di sfondo </td> 
   <td colname="2"> <p>Opacità della cella del carattere di sfondo. </p> <p>Espressa come percentuale da 0 (completamente trasparente) a 100 (completamente opaca). <span class="codeph"> DEFAULT_OPACITY </span> per lo sfondo è 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità riempimento </td> 
   <td colname="2"> <p>Opacità dello sfondo della finestra della didascalia. </p> <p>Espressa come percentuale da 0 (completamente trasparente) a 100 (completamente opaca). <span class="codeph"> DEFAULT_OPACITY </span> per il riempimento è 0. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Esempi di formattazione delle didascalie {#examples-caption-formatting}

È possibile specificare la formattazione dei sottotitoli codificati.

**Esempio 1: Specificare in modo esplicito i valori di formato**

```java
private final MediaPlayer.PlaybackEventListener  
  _playbackEventListener = new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder(TextFormat.Font.DEFAULT, 
        TextFormat.Size.DEFAULT, 
        TextFormat.FontEdge.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY).toTextFormat(); 
        mediaPlayer.setCCStyle(tf); 
        ... 
    } 
} 
```

**Esempio 2: Specificare i valori di formato nei parametri**

```java
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param size 
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
public TextFormatBuilder( 
    Font font, Size size, FontEdge fontEdge, 
    Color fontColor, Color backgroundColor,  
    Color fillColor, Color edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat toTextFormat(); 
 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public TextFormatBuilder setFont(Font font); 
... 
```
