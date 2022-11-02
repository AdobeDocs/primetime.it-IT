---
description: È possibile implementare una barra di controllo con supporto DVR per VOD e streaming live. Il supporto DVR include il concetto di una finestra ricercabile e il punto live del cliente.
title: Costruire una barra di controllo migliorata per il DVR
exl-id: 8e70f03c-880a-48c5-8728-a4b967c19925
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Costruire una barra di controllo migliorata per il DVR{#construct-a-control-bar-enhanced-for-dvr}

È possibile implementare una barra di controllo con supporto DVR per VOD e streaming live. Il supporto DVR include il concetto di una finestra ricercabile e il punto live del cliente.

* Per VOD, la lunghezza della finestra ricercabile corrisponde alla durata dell’intera risorsa.
* Per lo streaming dal vivo, la lunghezza della finestra DVR (ricercabile) è definita come l&#39;intervallo di tempo che inizia dalla finestra di riproduzione dal vivo e termina al punto dal vivo del client.

   Il punto live del client viene calcolato sottraendo la lunghezza del buffered dall&#39;estremità della finestra live. La durata di destinazione è un valore maggiore o uguale alla durata massima di un frammento nel manifesto.

   Il valore predefinito è 10000 ms.

   La barra di controllo per la riproduzione in diretta supporta il DVR posizionando prima il pollice nel punto di attivazione del client all&#39;avvio della riproduzione e visualizzando una regione che contrassegna l&#39;area in cui la ricerca non è consentita.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. Per implementare una barra di controllo con supporto DVR, segui i passaggi per visualizzare una barra di scorrimento ricerca, con alcune differenze minori:

   * È possibile scegliere di implementare una barra di controllo mappata solo per l&#39;intervallo ricercabile anziché per l&#39;intervallo di riproduzione. Qualsiasi interazione dell’utente per la ricerca può essere considerata sicura nell’intervallo ricercabile.
   * È possibile scegliere di implementare una barra di controllo mappata per l&#39;intervallo di riproduzione, ma che visualizza anche l&#39;intervallo ricercabile.

      Per una barra di controllo:
   1. Aggiungi una sovrapposizione alla barra di controllo che rappresenta l’intervallo di riproduzione.
   1. Quando l’utente inizia a cercare, controlla se la posizione di ricerca desiderata si trova nell’intervallo ricercabile utilizzando `MediaPlayer.seekableRange` proprietà.

      Ad esempio:

      ```
      var desiredPosition:Number = // TODO : choose a value 
      
      private function onStatusChange(event:MediaPlayerStatusChangeEvent):void { 
          switch(event.status) { 
              case MediaPlayerStatus.PREPARED: 
                  _mediaPlayer.prepareToPlay(desiredPosition); 
          } 
      }
      ```

      Puoi anche scegliere di cercare il punto attivo del cliente utilizzando `MediaPlayer.LIVE_POINT` costante.

      ```
      private function onSeekToLiveClick(event:MouseEvent):void { 
          _player.seek(DefaultMediaPlayer.LIVE_POINT); 
      }
      ```
