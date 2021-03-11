---
description: Lo stato del lettore multimediale determina quali azioni sono legali.
title: Ciclo di vita e stati dell’oggetto MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---


# Ciclo di vita e stati dell&#39;oggetto MediaPlayer{#lifecycle-and-statuses-of-the-mediaplayer-object}

Lo stato del lettore multimediale determina quali azioni sono legali.

Per lavorare con gli stati del lettore multimediale:

* È possibile recuperare lo stato corrente dell&#39;oggetto `MediaPlayer` con `MediaPlayer.getStatus()`.

* L&#39;elenco degli stati è definito nell&#39;enum [MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/com/adobe/mediacore/MediaPlayerStatus.html) .

Diagramma di transizione dello stato per il ciclo di vita di un&#39;istanza `MediaPlayer`:

<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

La tabella seguente fornisce dettagli sul ciclo di vita e sugli stati del lettore multimediale:

<table id="table_82757A0043EB4AACA474E6B30326A6B7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Stato </th> 
   <th colname="col2" class="entry"> Si verifica quando </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> INATTIVO </td> 
   <td colname="col2"> <p>Stato iniziale del lettore multimediale. Il lettore viene creato ed è in attesa di specificare un elemento del lettore multimediale. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INIZIALIZZAZIONE </td> 
   <td colname="col2"> <p>L'applicazione chiama <span class="codeph"> MediaPlayer.replaceCurrentItem() </span>. </p> <p>Caricamento dell'elemento del lettore multimediale in corso. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INIZIALIZZATO </td> 
   <td colname="col2"> <p>TVSDK: impostazione dell'elemento del lettore multimediale completata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PREPARAZIONE </td> 
   <td colname="col2"> <p>L'applicazione chiama <span class="codeph"> MediaPlayer.PrepareToPlay() </span>. Il lettore multimediale sta caricando l'elemento del lettore multimediale ed eventuali risorse associate. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PREPARATO </td> 
   <td colname="col2"> <p>TVSDK ha preparato il flusso multimediale e ha tentato di eseguire la risoluzione degli annunci e l'inserimento degli annunci (se abilitato). Il contenuto viene preparato e gli annunci sono stati inseriti nella timeline oppure la procedura dell’annuncio non è riuscita. </p> <p>È possibile iniziare il buffering o la riproduzione. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> RIPRODUZIONE/PAUSA </td> 
   <td colname="col2"> <p>Quando l'applicazione riproduce e mette in pausa il contenuto multimediale, il lettore multimediale si sposta tra questi stati. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> SOSPESO </td> 
   <td colname="col2"> <p>Se l'applicazione si allontana dalla riproduzione, spegne il dispositivo o cambia le applicazioni durante la riproduzione o la pausa del lettore, il lettore multimediale viene sospeso e le risorse vengono rilasciate. </p> <p>Se si richiama <span class="codeph"> MediaPlayer.restore() </span>, il lettore viene ripristinato allo stato in cui si trovava prima della sospensione. L'eccezione è che se il lettore è SEEKING quando viene chiamato sospeso, il lettore viene messo in pausa e quindi SOSPESO. </p> <p>Importante:  <p>Ricorda le seguenti informazioni: 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">Il <span class="codeph"> MediaPlayer </span> chiama automaticamente <span class="codeph"> sospende </span> solo quando l'oggetto di superficie utilizzato da <span class="codeph"> MediaPlayerView </span> viene distrutto. </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">Il <span class="codeph"> MediaPlayer </span> chiama automaticamente <span class="codeph"> restore() </span> solo quando viene creato un nuovo oggetto di superficie utilizzato da <span class="codeph"> MediaPlayerView </span>. </li> 
      </ul> </p> </p> <p>Se desideri sempre che la riproduzione venga messa in pausa quando MediaPlayer viene ripristinato, chiedi all'applicazione <span class="codeph"> MediaPlayer.pause() </span> nel metodo <span class="codeph"> onPause() dell'attività Android </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> COMPLETO </td> 
   <td colname="col2"> <p>Il lettore ha raggiunto la fine del flusso e la riproduzione si è arrestata. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> RILASCIATO </td> 
   <td colname="col2"> <p>L'applicazione ha rilasciato il lettore multimediale, che rilascia anche le risorse associate. Non puoi più utilizzare questa istanza. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ERRORE </td> 
   <td colname="col2"> <p>Errore durante il processo. Un errore potrebbe influire anche sulle operazioni che l'applicazione può eseguire in seguito. Per ulteriori informazioni, consulta <a href="../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-error-handling-set-up.md" format="dita" scope="local"> Configurare la gestione degli errori </a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>È possibile utilizzare lo stato per fornire un feedback sul processo, ad esempio un&#39;icona che ruota in attesa della successiva modifica dello stato, oppure per eseguire i passaggi successivi durante la riproduzione del supporto, ad esempio l&#39;attesa dello stato appropriato prima di chiamare il metodo successivo.

Ad esempio:

```java
mediaPlayer.addEventListener(MediaPlayerEvent STATUS_CHANGED, new StatusChangeEventListener() { 
    @Override  
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        switch(event.getStatus()) { 
            case INITIALIZED: 
                mediaPlayer.prepareToPlay(); 
                break; 
            case PREPARING: 
                showBufferingSpinner(); 
                break; 
            case PREPARED: 
                hideBufferingSpinner(); 
                mediaPlayer.play(); 
                break; 
            ...                
        } 
        ... 
    } 
}); 
```
