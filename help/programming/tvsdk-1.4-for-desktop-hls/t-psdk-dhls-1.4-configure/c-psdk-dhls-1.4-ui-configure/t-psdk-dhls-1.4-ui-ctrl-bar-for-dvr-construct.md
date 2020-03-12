---
description: È possibile implementare una barra di controllo con supporto DVR per VOD e streaming dal vivo. Il supporto DVR include il concetto di una finestra ricercabile e il punto attivo del cliente.
seo-description: È possibile implementare una barra di controllo con supporto DVR per VOD e streaming dal vivo. Il supporto DVR include il concetto di una finestra ricercabile e il punto attivo del cliente.
seo-title: Costruire una barra di controllo migliorata per il DVR
title: Costruire una barra di controllo migliorata per il DVR
uuid: 08f943e8-90da-4860-92dd-dd289fd68cba
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Costruire una barra di controllo migliorata per il DVR{#construct-a-control-bar-enhanced-for-dvr}

È possibile implementare una barra di controllo con supporto DVR per VOD e streaming dal vivo. Il supporto DVR include il concetto di una finestra ricercabile e il punto attivo del cliente.

* Per VOD, la lunghezza della finestra ricercabile corrisponde alla durata dell’intera risorsa.
* Per lo streaming dal vivo, la lunghezza della finestra DVR (ricercabile) è definita come l&#39;intervallo di tempo che inizia dalla finestra di riproduzione dal vivo e termina al punto attivo del client.

   Il punto attivo del client viene calcolato sottraendo la lunghezza del buffer dall&#39;estremità della finestra dal vivo. La durata di destinazione è un valore maggiore o uguale alla durata massima di un frammento nel manifesto.

   Il valore predefinito è 10000 ms.

   La barra di controllo per la riproduzione dal vivo supporta il DVR posizionando prima il pollice nel punto di vita del client all&#39;avvio della riproduzione e visualizzando un&#39;area che contrassegna l&#39;area in cui non è consentita la ricerca.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width=&quot;684&quot;}

1. Per implementare una barra di controllo con supporto DVR, seguite i passaggi per visualizzare una barra di scorrimento ricerca, con alcune differenze minori:

   * Potete scegliere di implementare una barra di controllo mappata solo per l’intervallo ricercabile invece che per l’intervallo di riproduzione. Qualsiasi interazione dell&#39;utente per la ricerca può essere considerata sicura nell&#39;intervallo ricercabile.
   * Potete scegliere di implementare una barra di controllo mappata per l’intervallo di riproduzione, ma che visualizzi anche l’intervallo ricercabile.

      Per una barra di controllo:
   1. Aggiungete una sovrapposizione alla barra di controllo che rappresenta l’intervallo di riproduzione.
   1. Quando l&#39;utente inizia a cercare, controllate se la posizione di ricerca desiderata si trova all&#39;interno dell&#39;intervallo ricercabile utilizzando la `MediaPlayer.seekableRange` proprietà.

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

      È inoltre possibile scegliere di cercare il punto attivo del client utilizzando la `MediaPlayer.LIVE_POINT` costante.

      ```
      private function onSeekToLiveClick(event:MouseEvent):void { 
          _player.seek(DefaultMediaPlayer.LIVE_POINT); 
      }
      ```


