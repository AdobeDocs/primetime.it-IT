---
description: È possibile fornire informazioni sullo stile per le tracce di sottotitoli codificati utilizzando la classe TextFormat, che imposta lo stile per i sottotitoli codificati visualizzati dal lettore.
title: Controlla lo stile dei sottotitoli
exl-id: fa96f9f5-f709-4749-90c8-cf237cf074c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '853'
ht-degree: 0%

---

# Controlla lo stile dei sottotitoli {#control-closed-caption-styling}

È possibile fornire informazioni sullo stile per le tracce di sottotitoli codificati utilizzando la classe TextFormat, che imposta lo stile per i sottotitoli codificati visualizzati dal lettore.

Questa classe racchiude informazioni sullo stile dei sottotitoli codificati, ad esempio il tipo di carattere, la dimensione, il colore e l&#39;opacità dello sfondo.

## Imposta stili sottotitoli codificati {#section_C9B5E75C70DD42E59DC4DD0F308C8216}

È possibile applicare uno stile al testo con sottotitoli codificati con i metodi TVSDK.

1. Attendi che il lettore multimediale si trovi almeno nel `PREPARED` stato.
1. Creare un `TextFormatBuilder` dell&#39;istanza.

   Potete specificare tutti i parametri di stile dei sottotitoli o impostarli in un secondo momento.

   TVSDK incapsula le informazioni sullo stile dei sottotitoli nella `TextFormat` di rete. Il `TextFormatBuilder` La classe crea oggetti che implementano questa interfaccia.

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

1. Per ottenere un riferimento a un oggetto che implementa `TextFormat` , chiama il `TextFormatBuilder.toTextFormat` metodo pubblico.

   >[!NOTE]
   >
   >Questo restituisce un `TextFormat` oggetto che può essere applicato al lettore multimediale.

   ```java
   public TextFormat toTextFormat()
   ```

1. È possibile ottenere le impostazioni di stile sottotitoli correnti eseguendo una delle operazioni seguenti:

   * Ottieni tutte le impostazioni di stile con `MediaPlayer.getCCStyle` Il valore restituito è un&#39;istanza del `TextFormat` di rete.

      ```java
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws MediaPlayerException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws MediaPlayerException;
      ```

   * Ottenere le impostazioni una alla volta tramite `TextFormat` metodi getter dell&#39;interfaccia.

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

   * Utilizzare il metodo setter `MediaPlayer.setCCStyle`, passaggio di un&#39;istanza di `TextFormat` Interfaccia:

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

   * Utilizza il `TextFormatBuilder` che definisce i singoli metodi di impostazione.

      Il `TextFormat` L&#39;interfaccia definisce un oggetto immutabile in modo che esistano solo metodi getter e nessun setter. È possibile impostare i parametri di stile dei sottotitoli solo con `TextFormatBuilder` classe:

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
      >**Impostazioni colore:** In Android TVSDK 2.X, è stato apportato un miglioramento allo stile dei colori dei sottotitoli. Questo miglioramento consente di impostare i colori dei sottotitoli codificati utilizzando una stringa esadecimale che rappresenta i valori dei colori RGB. La rappresentazione colore esadecimale RGB è la nota stringa da 6 byte utilizzata in applicazioni come Photoshop:
      >
      >* FFFFFF = Nero
      >* 000000 = bianco
      >* FF0000 = rosso
      >* 00FF00 = Verde
      >* 0000FF = Blu

      >
      >e così via.
      >
      >Nell&#39;applicazione, ogni volta che trasmettete le informazioni sullo stile del colore a `TextFormatBuilder`, si utilizza ancora il `Color` come prima, ma ora è necessario aggiungere `getValue()` al colore per ottenere il valore come stringa. Ad esempio:
      >
      >
      ```
      >tfb = tfb.setBackgroundColor(TextFormat.Color.RED <b>.getValue()</b>);
      >```

Poiché l&#39;impostazione dello stile sottotitoli è un&#39;operazione asincrona, la visualizzazione delle modifiche sullo schermo potrebbe richiedere alcuni secondi.

## Opzioni di stile sottotitoli codificati {#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

È possibile specificare diverse opzioni di stile per i sottotitoli, che sostituiscono le opzioni di stile dei sottotitoli originali.

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
  <tr rowsep="1"> 
   <td colname="1"> Interno inferiore </td> 
   <td colname="2"> <p>Distanza verticale dalla parte inferiore della finestra dei sottotitoli da evitare. </p> <p>Espresso come percentuale dell'altezza della finestra dei sottotitoli (ad esempio, "20%") o come numero di pixel (ad esempio, "20"). </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> Area utile </td> 
   <td colname="2"> <p>Area compresa tra 0% e 25% intorno al bordo dello schermo in cui i sottotitoli non verranno visualizzati. </p> <p>Per impostazione predefinita, l'area di sicurezza per WebVTT è 0%. Questa impostazione consente all'applicazione di ignorare tale impostazione predefinita. Se vengono forniti due valori, ad esempio la stringa "10%,20%", il primo valore è l’area di sicurezza orizzontale e il secondo valore è l’area di sicurezza verticale. Se viene fornito un valore, ad esempio la stringa "15%", sia l'asse verticale che l'asse orizzontale utilizzano l'area di sicurezza specificata. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Esempi di formattazione dei sottotitoli {#section_58E8E82494EC4683B010FFDE67485CF9}

Di seguito sono riportati alcuni esempi che mostrano come specificare la formattazione dei sottotitoli.

**Esempio 1: specificare esplicitamente i valori di formato**

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
