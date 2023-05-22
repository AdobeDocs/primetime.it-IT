---
description: È possibile implementare una barra di controllo con supporto DVR per VOD e streaming live. Il supporto DVR include il concetto di finestra ricercabile e il punto di attivazione del client.
title: Creare una barra di controllo ottimizzata per DVR
exl-id: 8e70f03c-880a-48c5-8728-a4b967c19925
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Creare una barra di controllo ottimizzata per DVR{#construct-a-control-bar-enhanced-for-dvr}

È possibile implementare una barra di controllo con supporto DVR per VOD e streaming live. Il supporto DVR include il concetto di finestra ricercabile e il punto di attivazione del client.

* Per VOD, la lunghezza della finestra ricercabile corrisponde alla durata dell’intera risorsa.
* Per lo streaming live, la lunghezza della finestra del DVR (ricercabile) è definita come l’intervallo di tempo che inizia dalla finestra di riproduzione live e termina nel punto live del client.

   Il punto di attivazione del client viene calcolato sottraendo la lunghezza nel buffer dalla fine della finestra attiva. La durata target è un valore maggiore o uguale alla durata massima di un frammento nel manifesto.

   Il valore predefinito è 10000 ms.

   La barra di controllo per la riproduzione dal vivo supporta DVR posizionando prima il pollice in corrispondenza del punto attivo del client all’avvio della riproduzione e visualizzando una regione che contrassegna l’area in cui non è consentita la ricerca.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. Per implementare una barra di controllo con supporto DVR, attenersi alla procedura descritta di seguito per visualizzare una barra di scorrimento di ricerca, con alcune lievi differenze:

   * Puoi scegliere di implementare una barra di controllo mappata solo per l’intervallo ricercabile anziché per l’intervallo di riproduzione. Qualsiasi interazione dell’utente per la ricerca può essere considerata sicura nell’intervallo ricercabile.
   * Puoi scegliere di implementare una barra di controllo mappata per l’intervallo di riproduzione, ma che visualizzi anche l’intervallo ricercabile.

      Per una barra di controllo:
   1. Aggiungi una sovrapposizione alla barra di controllo che rappresenta l’intervallo di riproduzione.
   1. Quando l’utente inizia a cercare, verifica se la posizione di ricerca desiderata si trova all’interno dell’intervallo ricercabile utilizzando `MediaPlayer.seekableRange` proprietà.

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

      Puoi anche scegliere di effettuare una ricerca nel punto di attivazione del client utilizzando `MediaPlayer.LIVE_POINT` costante.

      ```
      private function onSeekToLiveClick(event:MouseEvent):void { 
          _player.seek(DefaultMediaPlayer.LIVE_POINT); 
      }
      ```
