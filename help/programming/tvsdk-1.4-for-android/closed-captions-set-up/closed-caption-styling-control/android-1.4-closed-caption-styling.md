---
description: È possibile fornire informazioni sullo stile per le tracce a didascalia chiusa utilizzando la classe TextFormat. Questo imposta lo stile dei sottotitoli codificati visualizzati dal lettore.
title: Controllare lo stile dei sottotitoli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# Controllare lo stile dei sottotitoli {#control-closed-caption-styling-overview}

È possibile fornire informazioni sullo stile per le tracce a didascalia chiusa utilizzando la classe TextFormat. Questo imposta lo stile dei sottotitoli codificati visualizzati dal lettore.

Questa classe racchiude informazioni sullo stile dei sottotitoli, quali tipo di font, dimensioni, colore e opacità dello sfondo. Una classe helper associata, `TextFormatBuilder`, facilita l&#39;utilizzo delle impostazioni di stile dei sottotitoli.

## Impostare gli stili di sottotitoli {#set-closed-caption-styles}

È possibile personalizzare lo stile del testo a didascalia chiusa con i metodi TVSDK.

1. Attendi che il lettore multimediale sia almeno nello stato PREPARATO.
1. Crea un&#39;istanza `TextFormatBuilder`.

   Ora puoi fornire tutti i parametri di stile dei sottotitoli o impostarli in un secondo momento.

   TVSDK incapsula le informazioni sullo stile dei sottotitoli nell&#39;interfaccia `TextFormat`. La classe `TextFormatBuilder` crea oggetti che implementano questa interfaccia.

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

1. Per ottenere un riferimento a un oggetto che implementa l&#39;interfaccia `TextFormat`, chiamare il metodo pubblico `TextFormatBuilder.toTextFormat` .

   Restituisce un oggetto `TextFormat` che può essere applicato al lettore multimediale.

   ```java
   public TextFormat toTextFormat()
   ```

1. Facoltativamente, ottenere le impostazioni correnti dello stile dei sottotitoli codificati eseguendo una delle operazioni seguenti:

   * Ottieni tutte le impostazioni dello stile con `MediaPlayer.getCCStyle`.

      Il valore restituito è un&#39;istanza dell&#39;interfaccia `TextFormat`.

      ```js
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws IllegalStateException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws IllegalStateException;
      ```

   * Ottieni le impostazioni una alla volta tramite i metodi getter dell&#39;interfaccia `TextFormat` .

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

1. Per modificare le impostazioni dello stile, effettuare una delle seguenti operazioni:

   >[!NOTE]
   >
   >Non è possibile modificare le dimensioni delle didascalie WebVTT.

   * Utilizzare il metodo setter `MediaPlayer.setCCStyle`, passando un&#39;istanza dell&#39;interfaccia `TextFormat`:

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

   * Utilizzare la classe `TextFormatBuilder`, che definisce i singoli metodi di setter.

      L&#39;interfaccia `TextFormat` definisce un oggetto immutabile in modo che esistano solo metodi getter e senza setter. È possibile impostare i parametri di stile dei sottotitoli solo con la classe `TextFormatBuilder` :

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

L’impostazione dello stile dei sottotitoli è un’operazione asincrona, pertanto potrebbero essere necessari fino a pochi secondi affinché le modifiche vengano visualizzate sullo schermo.

## Opzioni per lo stile dei sottotitoli {#closed-caption-styling-options}

È possibile specificare diverse opzioni di stile per le didascalie e queste opzioni sostituiscono le opzioni di stile nelle didascalie originali

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

>[!TIP]
>
>Nelle opzioni che definiscono i valori predefiniti (ad esempio, DEFAULT), tale valore si riferisce all’impostazione quando la didascalia è stata originariamente specificata.

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
   <td colname="1"> Bordo font </td> 
   <td colname="2"> <p>Effetto utilizzato per lo spigolo del font, ad esempio sollevato o nessuno. </p> <p>Può essere impostato solo su un valore definito dall'enumerazione <span class="codeph"> TextFormat.FontEdge </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore font </td> 
   <td colname="2"> <p>Il colore del font. </p> <p>Può essere impostato solo su un valore definito dall'enumerazione <span class="codeph"> TextFormat.Color </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore bordo </td> 
   <td colname="2"> <p>Colore dell'effetto bordo. </p> <p>Può essere impostato su uno qualsiasi dei valori disponibili per il colore del font. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore di sfondo </td> 
   <td colname="2"> <p>Colore della cella del carattere di sfondo. </p> <p>Può essere impostato solo sui valori disponibili per il colore del font. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore riempimento </td> 
   <td colname="2"> <p>Colore dello sfondo della finestra in cui si trova il testo. </p> <p>Può essere impostato su uno qualsiasi dei valori disponibili per il colore del font. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> opacità del carattere </td> 
   <td colname="2"> <p>opacità del testo. </p> <p>Espresso in percentuale da 0 (completamente trasparente) a 100 (completamente opaco). <span class="codeph"> DEFAULT_OPACITY  </span> per il font è 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità di sfondo </td> 
   <td colname="2"> <p>opacità della cella del carattere di sfondo. </p> <p>Espresso in percentuale da 0 (completamente trasparente) a 100 (completamente opaco). <span class="codeph"> DEFAULT_OPACITY  </span> per lo sfondo è 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Opacità di riempimento </td> 
   <td colname="2"> <p>opacità dello sfondo della finestra della didascalia. </p> <p>Espresso in percentuale da 0 (completamente trasparente) a 100 (completamente opaco). <span class="codeph"> DEFAULT_OPACITY  </span> per il riempimento è 0. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Esempi di formattazione delle didascalie {#examples-caption-formatting}

È possibile specificare la formattazione dei sottotitoli.

**Esempio 1: Specificare esplicitamente i valori di formato**

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
