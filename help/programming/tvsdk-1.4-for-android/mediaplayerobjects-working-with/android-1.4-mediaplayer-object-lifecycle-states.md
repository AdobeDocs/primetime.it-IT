---
description: Dal momento in cui create l’istanza MediaPlayer al momento in cui viene terminata (riutilizzata o rimossa), questa istanza completa una serie di transizioni tra stati.
seo-description: Dal momento in cui create l’istanza MediaPlayer al momento in cui viene terminata (riutilizzata o rimossa), questa istanza completa una serie di transizioni tra stati.
seo-title: ciclo di vita dell’oggetto MediaPlayer
title: ciclo di vita dell’oggetto MediaPlayer
uuid: 6670a30c-7053-4754-bc36-6bb8590c001d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# ciclo di vita dell’oggetto MediaPlayer{#mediaplayer-object-lifecycle}

Dal momento in cui create l’istanza MediaPlayer al momento in cui viene terminata (riutilizzata o rimossa), questa istanza completa una serie di transizioni tra stati.

Alcune operazioni sono consentite solo quando il lettore si trova in uno stato particolare. Ad esempio, la chiamata `play` in `IDLE` non è consentita. Potete richiamare questo stato solo dopo che il lettore ha raggiunto lo `PREPARED` stato.

Per utilizzare gli stati:

* È possibile recuperare lo stato corrente dell&#39; `MediaPlayer` oggetto con `MediaPlayer.getStatus`.

   ```java
   PlayerState getStatus() throws IllegalStateException;
   ```

* L&#39;elenco degli stati è definito in `MediaPlayer.PlayerState`.

Diagramma di transizione dello stato per il ciclo di vita di un’ `MediaPlayer` istanza:
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

La tabella seguente fornisce ulteriori dettagli:

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> MediaPlayer.PlayerState </th> 
   <th colname="col2" class="entry"> Si verifica quando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> IDLE </span> </td> 
   <td colname="col2"> <p>L’applicazione ha richiesto un nuovo lettore multimediale chiamando <span class="codeph"> DefaultMediaPlayer.create </span>. Il nuovo lettore creato è in attesa di specificare un elemento del lettore multimediale. Questo è lo stato iniziale del lettore multimediale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INIZIALIZZAZIONE </span> </td> 
   <td colname="col2"> <p>L’applicazione chiamata <span class="codeph"> MediaPlayer.replaceCurrentItem </span>e il lettore multimediale si sta caricando. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INIZIALIZZATO </span> </td> 
   <td colname="col2"> <p>TVSDK ha impostato correttamente l'elemento del lettore multimediale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARAZIONE </span> </td> 
   <td colname="col2"> <p>L’applicazione chiamata <span class="codeph"> MediaPlayer.PreparareToPlay </span>. Il lettore multimediale sta caricando l'elemento del lettore multimediale e le risorse associate. </p> <p>Suggerimento:  È possibile che si verifichi una certa bufferizzazione del supporto principale. </p> <p>TVSDK sta preparando il flusso multimediale e sta tentando di eseguire la risoluzione e l'inserimento di annunci (se attivato). </p> <p>Suggerimento:  Per impostare l’ora di inizio su un valore diverso da zero, invoca <span class="codeph"> PrepareToPlay(startTime) </span> con l’ora in millisecondi. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARATO </span> </td> 
   <td colname="col2"> <p>Il contenuto è preparato e gli annunci sono stati inseriti nella timeline, oppure la procedura di annuncio non è riuscita. È possibile avviare il buffering o la riproduzione. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> GIOCO </span> </td> 
   <td colname="col2"> <p>L’applicazione ha chiamato <span class="codeph"> play </span>, quindi TVSDK sta tentando di riprodurre il video. Prima della riproduzione del video potrebbe verificarsi un buffering. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> IN PAUSA </span> </td> 
   <td colname="col2"> <p>Quando l’applicazione riproduce e mette in pausa il supporto, il lettore multimediale si sposta tra questo stato e PLAYING. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> SOSPESO </span> </td> 
   <td colname="col2"> <p>L’applicazione si è allontanata dalla riproduzione, ha spento il dispositivo o ha modificato le applicazioni durante la riproduzione o la pausa del lettore. Il lettore multimediale è stato sospeso e le risorse sono state rilasciate. Per continuare, ripristinare il lettore multimediale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> COMPLETE </span> </td> 
   <td colname="col2"> <p>Il lettore ha raggiunto la fine del flusso e la riproduzione si è interrotta. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RILASCIATO </span> </td> 
   <td colname="col2"> <p>L'applicazione ha rilasciato il lettore multimediale, che rilascia anche tutte le risorse associate. Non è più possibile utilizzare questa istanza </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ERRORE </span> </td> 
   <td colname="col2"> <p>Errore durante il processo. Un errore potrebbe inoltre influire sulle operazioni che l'applicazione potrà eseguire successivamente. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>Potete utilizzare lo stato per fornire un feedback sul processo (ad esempio, una casella di selezione in attesa della successiva modifica dello stato) o per effettuare il passaggio successivo durante la riproduzione del supporto, ad esempio in attesa dello stato appropriato prima di chiamare il metodo successivo.

Ad esempio:

```java
@Override 
public void onStateChanged(MediaPlayer.PlayerState state,  
                           MediaPlayerNotification notification) { 
   switch (state) { 
      // It is recommended that you call prepareToPlay() after receiving  
      // the INITIALIZED state. 
      case INITIALIZED: 
         _mediaPlayer.prepareToPlay(); 
         break; 
      case PREPARING: 
         showBufferingSpinner(); 
         break; 
      case PREPARED: 
         hideBufferingSpinner(); 
      ..... 
    } 
}
```

