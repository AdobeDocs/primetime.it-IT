---
description: È possibile implementare una barra di controllo con supporto DVR per VOD e streaming live. Il supporto DVR include il concetto di finestra ricercabile e il punto di attivazione del client.
title: Creare una barra di controllo ottimizzata per DVR
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# Creare una barra di controllo ottimizzata per DVR {#construct-a-control-bar-enhanced-for-dvr}

È possibile implementare una barra di controllo con supporto DVR per VOD e streaming live. Il supporto DVR include il concetto di finestra ricercabile e il punto di attivazione del client.

* Per VOD, la lunghezza della finestra ricercabile corrisponde alla durata dell’intera risorsa.
* Per lo streaming live, la lunghezza della finestra del DVR (ricercabile) è definita come l’intervallo di tempo che inizia dalla finestra di riproduzione live e termina nel punto live del client.

  Tenere presenti le seguenti informazioni:

   * Il punto di attivazione del client viene calcolato sottraendo la lunghezza nel buffer dalla fine della finestra attiva.

     La durata target è un valore maggiore o uguale alla durata massima di un frammento nel manifesto.
   * Il valore predefinito è 10000 ms.
   * La barra di controllo per la riproduzione dal vivo supporta DVR posizionando prima il pollice in corrispondenza del punto attivo del client all’avvio della riproduzione e visualizzando una regione che contrassegna l’area in cui non è consentita la ricerca.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. Per implementare una barra di controllo con supporto DVR, seguire i passaggi descritti in [Visualizza una barra di scorrimento di ricerca con la posizione di riproduzione corrente...](../../../tvsdk-2.7-for-android/content-playback-options/ui-configure/t-psdk-android-2.7-ui-seek-scrub-bar-display.md) con le seguenti differenze:

   * È possibile implementare una barra di controllo mappata solo per l’intervallo ricercabile anziché per l’intervallo di riproduzione.

     Qualsiasi interazione dell’utente per la ricerca può essere considerata sicura nell’intervallo ricercabile.
   * Puoi implementare una barra di controllo mappata per l’intervallo di riproduzione, ma che mostri anche l’intervallo ricercabile.

     Per una barra di controllo:

   1. Aggiungi una sovrapposizione alla barra di controllo che rappresenta l’intervallo di riproduzione.
   1. Quando l’utente inizia a cercare, verifica se la posizione di ricerca desiderata si trova all’interno dell’intervallo ricercabile utilizzando `MediaPlayer.getSeekableRange`.

      Ad esempio:

      ```java
      TimeRange seekableRange = _mediaPlayer.getSeekableRange(); 
      if (seekableRange.contains(desiredSeekPosition)) { 
          _mediaPlayer.seek(desiredPosition); 
      }
      ```

      Puoi anche scegliere di effettuare una ricerca nel punto di attivazione del client utilizzando `MediaPlayer.LIVE_POINT` costante.

      ```
      mediaPlayer.seek(MediaPlayer.LIVE_POINT);
      ```
