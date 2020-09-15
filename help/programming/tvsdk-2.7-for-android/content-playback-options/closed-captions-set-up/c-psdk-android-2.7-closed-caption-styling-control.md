---
description: È possibile fornire informazioni sullo stile per le tracce di sottotitoli codificati utilizzando la classe TextFormat, che imposta lo stile per le didascalie chiuse visualizzate dal lettore.
seo-description: È possibile fornire informazioni sullo stile per le tracce di sottotitoli codificati utilizzando la classe TextFormat, che imposta lo stile per le didascalie chiuse visualizzate dal lettore.
seo-title: Controllo dello stile dei sottotitoli codificati
title: Controllo dello stile dei sottotitoli codificati
uuid: fa4f637f-f13c-465d-8eee-5e66a6dd9db2
translation-type: tm+mt
source-git-commit: 4ccc99f1ad6536ceb5e09c898dba3f71fa2de3f3
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---


# Controllo dello stile dei sottotitoli codificati {#control-closed-caption-styling}

È possibile fornire informazioni sullo stile per le tracce di sottotitoli codificati utilizzando la classe TextFormat, che imposta lo stile per le didascalie chiuse visualizzate dal lettore.

Questa classe racchiude informazioni sullo stile dei sottotitoli codificati quali tipo di font, dimensione, colore e opacità dello sfondo.

## Impostare gli stili di didascalia {#section_C9B5E75C70DD42E59DC4DD0F308C8216}

Potete formattare il testo dei sottotitoli codificati con i metodi TVSDK.

1. Attendete che il lettore multimediale sia almeno nello `PREPARED` stato.
1. Create un&#39; `TextFormatBuilder` istanza.

   Potete fornire ora tutti i parametri di stile per i sottotitoli codificati o impostarli successivamente.

   TVSDK racchiude informazioni sullo stile dei sottotitoli codificati nell&#39; `TextFormat` interfaccia. La `TextFormatBuilder` classe crea oggetti che implementano questa interfaccia.

   ```java
   public TextFormatBuilder( 
      TextFormat.Font font, 
      TextFormat.Size size, 
      TextFormat.FontEdge fontEdge, 
      java.lang.String fontColor, 
      java.lang.String backgroundColor, 
      java.lang.String fillColor, 
      java.lang.String edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity 
      java.lang.String bottomInset, 
      java.lang.String safeArea)
   ```

1. Per ottenere un riferimento a un oggetto che implementa l&#39; `TextFormat` interfaccia, chiamare il metodo `TextFormatBuilder.toTextFormat` public.

   >[!NOTE]
   >
   >Questo restituisce un `TextFormat` oggetto che può essere applicato al lettore multimediale.

   ```java
   public TextFormat toTextFormat()
   ```

1. Facoltativamente, per ottenere le impostazioni correnti per lo stile dei sottotitoli codificati, effettuate una delle seguenti operazioni:

   * Ottenere tutte le impostazioni di stile con `MediaPlayer.getCCStyle` Il valore restituito è un&#39;istanza dell&#39; `TextFormat` interfaccia.

      ```java
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws MediaPlayerException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws MediaPlayerException;
      ```

   * Ottenete le impostazioni una alla volta tramite i metodi `TextFormat` getter dell&#39;interfaccia.

      ```java
      public java.lang.String getFontColor(); 
      public java.lang.String getBackgroundColor(); 
      public java.lang.String getFillColor(); // retrieve the font fill color 
      public java.lang.String getEdgeColor(); // retrieve the font edge color 
      public TextFormat.Size getSize(); // retrieve the font size 
      public TextFormat.FontEdge getFontEdge(); // retrieve the font edge type 
      public TextFormat.Font getFont(); // retrieve the font type 
      public int getFontOpacity(); 
      public int getBackgroundOpacity(); 
      public java.lang.String getBottomInset(java.lang.String bi); 
      public java.lang.String getSafeArea(java.lang.String sa);
      ```

1. Per modificare le impostazioni di stile, effettuare una delle seguenti operazioni:

   * Utilizzate il metodo setter `MediaPlayer.setCCStyle`, passando un&#39;istanza dell&#39; `TextFormat` interfaccia:

      ```java
      /** 
      * Sets the closed captioning style. Used to control the closed captioning font, 
      * size, color, edge and opacity.  
      * 
      * This method is safe to use even if the current media stream doesn't have closed 
      * captions. 
      * 
      * @param textFormat 
      * @throws MediaPlayerException 
      */ 
      public void setCCStyle(TextFormat textFormat) throws MediaPlayerException;
      ```

   * Utilizzare la `TextFormatBuilder` classe, che definisce i singoli metodi setter.

      L&#39; `TextFormat` interfaccia definisce un oggetto immutabile, quindi esistono solo metodi getter e nessun setter. È possibile impostare i parametri di stile dei sottotitoli codificati solo con la `TextFormatBuilder` classe:

      ```java
      // set font type 
      public void setFont(Font font)  
      public void setBackgroundColor(String backgroundColor) 
      public void setFillColor(String fillColor) 
      // set the font-edge color 
      public void setEdgeColor(String edgeColor)  
      // set the font size 
      public void setSize(Size size)  
      // set the font edge type 
      public void setFontEdge(FontEdge fontEdge)  
      public void setFontOpacity(int fontOpacity) 
      public void setBackgroundOpacity(int backgroundOpacity) 
      // set the font-fill opacity level 
      public void setFillOpacity(int fillOpacity)  
      public void setFontColor(String fontColor) 
      public void setBottomInset(String bi) 
      public void setSafeArea(String sa) 
      public void setTreatSpaceAsAlphaNum(bool)
      ```

      >[!IMPORTANT]
      >
      >**Impostazioni colore:** In Android TVSDK 2.X, è stato migliorato lo stile dei colori dei sottotitoli codificati. Questa funzione consente di impostare i colori dei sottotitoli codificati utilizzando una stringa esadecimale che rappresenta i valori di colore RGB. La rappresentazione del colore esadecimale RGB è la nota stringa a 6 byte utilizzata in applicazioni come Photoshop:
      >
      >    * FFFF = Nero
      >    * 000000 = Bianco
      >    * FF0000 = Rosso
      >    * 00FF00 = Verde
      >    * 0000FF = Blu

      >
      >e così via.
      >
      >Nell&#39;applicazione, ogni volta che trasmettete informazioni sullo stile del colore, `TextFormatBuilder`utilizzate comunque l&#39; `Color` enumerazione come precedente, ma ora dovete aggiungere `getValue()` al colore per ottenere il valore come una stringa. Ad esempio:
      >
      >
      ```
      >tfb = tfb.setBackgroundColor(TextFormat.Color.RED <b>.getValue()</b>);
      >```




L&#39;impostazione dello stile dei sottotitoli codificati è un&#39;operazione asincrona, pertanto la visualizzazione delle modifiche sullo schermo potrebbe richiedere alcuni secondi.

## Opzioni di stile dei sottotitoli codificati {#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

È possibile specificare diverse opzioni di stile delle didascalie, che sostituiscono le opzioni di stile nelle didascalie originali.

```java
public TextFormatBuilder( 
   Font font, 
   Size size, 
   FontEdge fontEdge, 
   String fontColor, 
   String backgroundColor, 
   String fillColor, 
   String edgeColor, 
   int fontOpacity, 
   int backgroundOpacity, 
   int fillOpacity,  
   String bottomInset 
   String safeArea)
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
  <tr rowsep="1"> 
   <td colname="1"> Margine inferiore </td> 
   <td colname="2"> <p>Distanza verticale dalla parte inferiore della finestra della didascalia per evitare la comparsa di didascalie. </p> <p>Espressa come percentuale dell'altezza della finestra della didascalia (ad esempio, "20%") o come numero di pixel (ad esempio, "20"). </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> Area di sicurezza </td> 
   <td colname="2"> <p>Un'area intorno al bordo dello schermo compresa tra 0% e 25% in cui le didascalie non verranno visualizzate. </p> <p>Per impostazione predefinita, l'area di sicurezza per WebVTT è 0%. Questa impostazione consente all'applicazione di ignorare tale impostazione predefinita. Se vengono forniti due valori, ad esempio la stringa "10%,20%", il primo valore è l'area di sicurezza orizzontale e il secondo valore è l'area di sicurezza verticale. Se viene fornito un valore, ad esempio la stringa "15%", sia gli assi verticali che orizzontali utilizzano l'area di sicurezza specificata. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Esempi di formattazione delle didascalie {#section_58E8E82494EC4683B010FFDE67485CF9}

Di seguito sono riportati alcuni esempi che mostrano come specificare la formattazione dei sottotitoli codificati.

**Esempio 1: Specificare in modo esplicito i valori di formato**

```java
private final MediaPlayer.PlaybackEventListener _playbackEventListener = 
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder( 
            TextFormat.Font.DEFAULT, 
            TextFormat.Size.DEFAULT, 
            TextFormat.FontEdge.DEFAULT, 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
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
public  
<b>TextFormatBuilder</b>( 
    Font font, Size size, FontEdge fontEdge, 
    String fontColor, String backgroundColor,  
    String fillColor, String edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat  
<b>toTextFormat</b>(); 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public  
<b>TextFormatBuilder</b> setFont(Font font); 
...
```
