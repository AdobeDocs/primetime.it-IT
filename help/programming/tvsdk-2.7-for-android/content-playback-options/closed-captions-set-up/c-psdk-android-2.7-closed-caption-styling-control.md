---
description: È possibile fornire informazioni sullo stile per le tracce di didascalia chiusa utilizzando la classe TextFormat, che imposta lo stile per le didascalie chiuse visualizzate dal lettore.
title: Controllare lo stile dei sottotitoli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---


# Controllare lo stile dei sottotitoli {#control-closed-caption-styling}

È possibile fornire informazioni sullo stile per le tracce di didascalia chiusa utilizzando la classe TextFormat, che imposta lo stile per le didascalie chiuse visualizzate dal lettore.

Questa classe racchiude informazioni sullo stile dei sottotitoli codificati quali tipo di font, dimensioni, colore e opacità dello sfondo.

## Impostare gli stili di sottotitoli {#section_C9B5E75C70DD42E59DC4DD0F308C8216}

È possibile personalizzare lo stile del testo a didascalia chiusa con i metodi TVSDK.

1. Attendi che il lettore multimediale sia almeno nello stato `PREPARED`.
1. Crea un&#39;istanza `TextFormatBuilder`.

   Ora puoi fornire tutti i parametri di stile dei sottotitoli o impostarli in un secondo momento.

   TVSDK incapsula le informazioni sullo stile dei sottotitoli nell&#39;interfaccia `TextFormat`. La classe `TextFormatBuilder` crea oggetti che implementano questa interfaccia.

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

1. Per ottenere un riferimento a un oggetto che implementa l&#39;interfaccia `TextFormat`, chiamare il metodo pubblico `TextFormatBuilder.toTextFormat` .

   >[!NOTE]
   >
   >Restituisce un oggetto `TextFormat` che può essere applicato al lettore multimediale.

   ```java
   public TextFormat toTextFormat()
   ```

1. Facoltativamente, ottenere le impostazioni correnti dello stile dei sottotitoli codificati eseguendo una delle operazioni seguenti:

   * Ottieni tutte le impostazioni di stile con `MediaPlayer.getCCStyle` Il valore restituito è un&#39;istanza dell&#39;interfaccia `TextFormat`.

      ```java
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws MediaPlayerException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws MediaPlayerException;
      ```

   * Ottieni le impostazioni una alla volta tramite i metodi getter dell&#39;interfaccia `TextFormat` .

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

1. Per modificare le impostazioni dello stile, effettuare una delle seguenti operazioni:

   * Utilizzare il metodo setter `MediaPlayer.setCCStyle`, passando un&#39;istanza dell&#39;interfaccia `TextFormat`:

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

   * Utilizzare la classe `TextFormatBuilder`, che definisce i singoli metodi di setter.

      L&#39;interfaccia `TextFormat` definisce un oggetto immutabile in modo che esistano solo metodi getter e senza setter. È possibile impostare i parametri di stile dei sottotitoli solo con la classe `TextFormatBuilder` :

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
      >**Impostazioni colore:** in Android TVSDK 2.X, è stato migliorato lo stile del colore dei sottotitoli codificati. Il miglioramento consente di impostare i colori dei sottotitoli utilizzando una stringa esadecimale che rappresenta i valori di colore RGB. La rappresentazione del colore esadecimale RGB è la nota stringa a 6 byte utilizzata in applicazioni come Photoshop:
      >
      >* FFFF = nero
      >* 000000 = Bianco
      >* FF0000 = rosso
      >* 00FF00 = Verde
      >* 0000FF = Blu

      >
      >e così via.
      >
      >Nell&#39;applicazione, ogni volta che trasmetti informazioni sullo stile del colore a `TextFormatBuilder`, utilizzi comunque l&#39;enumerazione `Color` come prima, ma ora devi aggiungere `getValue()` al colore per ottenere il valore come stringa. Ad esempio:
      >
      >
      ```
      >tfb = tfb.setBackgroundColor(TextFormat.Color.RED <b>.getValue()</b>);
      >```




L’impostazione dello stile dei sottotitoli è un’operazione asincrona, pertanto potrebbero essere necessari fino a pochi secondi affinché le modifiche vengano visualizzate sullo schermo.

## Opzioni per lo stile dei sottotitoli {#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

È possibile specificare diverse opzioni di stile per le didascalie e queste opzioni sostituiscono le opzioni di stile nelle didascalie originali.

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
  <tr rowsep="1"> 
   <td colname="1"> Ingresso inferiore </td> 
   <td colname="2"> <p>Distanza verticale dalla parte inferiore della finestra della didascalia per evitare didascalie. </p> <p>Espresso come percentuale dell’altezza della finestra della didascalia (ad esempio, "20%") o come numero di pixel (ad esempio, "20"). </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> Area di sicurezza </td> 
   <td colname="2"> <p>Area intorno al bordo dello schermo compresa tra 0% e 25% in cui i sottotitoli non verranno visualizzati. </p> <p>Per impostazione predefinita, l’area di sicurezza per WebVTT è 0%. Questa impostazione consente all’applicazione di ignorare tale impostazione predefinita. Se vengono forniti due valori, ad esempio la stringa "10%,20%", il primo valore è l'area di sicurezza orizzontale e il secondo valore è l'area di sicurezza verticale. Se viene fornito un valore, ad esempio la stringa "15%", sia gli assi verticali che orizzontali utilizzano l'area di sicurezza specificata. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Esempi di formattazione delle didascalie {#section_58E8E82494EC4683B010FFDE67485CF9}

Di seguito sono riportati alcuni esempi che mostrano come specificare la formattazione dei sottotitoli codificati.

**Esempio 1: Specificare esplicitamente i valori di formato**

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
