---
description: È possibile fornire informazioni sullo stile dei brani con sottotitoli codificati utilizzando la classe TextFormat. Imposta lo stile per i sottotitoli che vengono visualizzati dal lettore.
title: Controlla lo stile dei sottotitoli
exl-id: 0083c141-9c03-46a2-902b-6e7eebaadea4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Controlla lo stile dei sottotitoli {#control-closed-caption-styling-overview}

È possibile fornire informazioni sullo stile dei brani con sottotitoli codificati utilizzando la classe TextFormat. Imposta lo stile per i sottotitoli che vengono visualizzati dal lettore.

Questa classe racchiude informazioni sullo stile dei sottotitoli codificati, ad esempio il tipo di carattere, la dimensione, il colore e l&#39;opacità dello sfondo. Una classe helper associata, `TextFormatBuilder`, facilita l&#39;utilizzo delle impostazioni di stile sottotitoli.

## Imposta stili sottotitoli codificati {#set-closed-caption-styles}

È possibile applicare uno stile al testo con sottotitoli codificati con i metodi TVSDK.

1. Attendere che il lettore multimediale sia almeno nello stato PREPARATO.
1. Creare un `TextFormatBuilder` dell&#39;istanza.

   Potete specificare tutti i parametri di stile dei sottotitoli o impostarli in un secondo momento.

   TVSDK incapsula le informazioni sullo stile dei sottotitoli nella `TextFormat` di rete. Il `TextFormatBuilder` La classe crea oggetti che implementano questa interfaccia.

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

1. Per ottenere un riferimento a un oggetto che implementa `TextFormat` , chiama il `TextFormatBuilder.toTextFormat` metodo pubblico.

   Questo restituisce un `TextFormat` oggetto che può essere applicato al lettore multimediale.

   ```java
   public TextFormat toTextFormat()
   ```

1. È possibile ottenere le impostazioni di stile sottotitoli correnti eseguendo una delle operazioni seguenti:

   * Ottieni tutte le impostazioni di stile con `MediaPlayer.getCCStyle`.

      Il valore restituito è un&#39;istanza del `TextFormat` di rete.

      ```js
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws IllegalStateException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws IllegalStateException;
      ```

   * Ottenere le impostazioni una alla volta tramite `TextFormat` metodi getter dell&#39;interfaccia.

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
   >Non è possibile modificare le dimensioni dei sottotitoli WebVTT.

   * Utilizzare il metodo setter `MediaPlayer.setCCStyle`, passaggio di un&#39;istanza di `TextFormat` Interfaccia:

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

   * Utilizza il `TextFormatBuilder` che definisce i singoli metodi di impostazione.

      Il `TextFormat` L&#39;interfaccia definisce un oggetto immutabile in modo che esistano solo metodi getter e nessun setter. È possibile impostare i parametri di stile dei sottotitoli solo con `TextFormatBuilder` classe:

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

Poiché l&#39;impostazione dello stile sottotitoli è un&#39;operazione asincrona, la visualizzazione delle modifiche sullo schermo potrebbe richiedere alcuni secondi.

## Opzioni di stile sottotitoli codificati {#closed-caption-styling-options}

È possibile specificare diverse opzioni di stile per i sottotitoli, che sostituiscono quelle dei sottotitoli originali

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
>Nelle opzioni che definiscono i valori predefiniti (ad esempio, DEFAULT), tale valore si riferisce all&#39;impostazione utilizzata quando la didascalia è stata specificata originariamente.

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
   <td colname="1"> Bordo font </td> 
   <td colname="2"> <p>Effetto utilizzato per il bordo del font, ad esempio in rilievo o nessuno. </p> <p>Può essere impostato solo su un valore definito da <span class="codeph"> TextFormat.FontEdge </span> enumerazione. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Colore font </td> 
   <td colname="2"> <p>Colore del carattere. </p> <p>Può essere impostato solo su un valore definito da <span class="codeph"> FormatoTesto.Colore </span> enumerazione. </p> </td> 
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
   <td colname="2"> <p>Colore dello sfondo della finestra in cui si trova il testo. </p> <p>Può essere impostato su uno qualsiasi dei valori disponibili per il colore del carattere. </p> </td> 
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

## Esempi di formattazione dei sottotitoli {#examples-caption-formatting}

È possibile specificare la formattazione dei sottotitoli.

**Esempio 1: specificare esplicitamente i valori di formato**

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

**Esempio 2: specificare i valori di formato nei parametri**

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
