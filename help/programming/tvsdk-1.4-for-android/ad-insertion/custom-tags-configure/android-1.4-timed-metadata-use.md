---
description: È possibile utilizzare TimedMetadata quando il tempo di riproduzione corrente corrisponde all'ora di inizio.
title: Usa metadati temporizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Usa metadati temporizzati {#use-timed-metadata}

È possibile utilizzare TimedMetadata quando il tempo di riproduzione corrente corrisponde all&#39;ora di inizio.

Per utilizzare i file salvati `TimedMetadata` durante la riproduzione, utilizza gli oggetti salvati `ArrayList` da [Archivia gli oggetti metadati temporizzati durante l’invio](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. Eseguire un timer ed eseguire ripetutamente una query sul tempo di riproduzione corrente.
1. Trova tutte le `TimedMetadata` oggetti con orari di inizio corrispondenti al tempo di riproduzione corrente.

   È possibile utilizzare questi oggetti per completare varie azioni.

   >[!IMPORTANT]
   >
   >Quando si controlla se il tempo di riproduzione corrente corrisponde a `TimedMetadata` oggetti, includi `shouldTriggerSubscribedTagEvent` come condizione.

   La timeline potrebbe cambiare a seguito di vari comportamenti pubblicitari. Ad esempio, una o più interruzioni pubblicitarie potrebbero essere spostate dalle posizioni originali sulla timeline, ma `shouldTriggerSubscribedTagEvent` garantisce che `TimeMetadata` l&#39;ora di inizio dell&#39;oggetto corrisponde all&#39;ora di riproduzione corrente.

   Ad esempio:

   ```java
    _playbackClockEventListener = new Clock.ClockEventListener() {
       @Override
       public void onTick(String name) {
           getActivity().runOnUiThread(new Runnable() {
               @Override
               public void run() {
                   /* handle timedmetadata object list  */ 
                   if (_mediaPlayer != null && _timedMetadataList != null && _timedMetadataList.size() > 0) {
                       if (_lastKnownStatus == MediaPlayer.PlayerState.PLAYING) {
                           long localTime = _mediaPlayer.getLocalTime();
                           Iterator<TimedMetadata> iterator = _timedMetadataList.iterator(); 
                           while (iterator.hasNext()) {
                               TimedMetadata timedMetadata = iterator.next();
                               long diff = localTime - timedMetadata.getTime();
                               if (diff >= 0 &&
                                   diff <= PLAYBACK_CLOCK_INTERVAL &&
                                   _mediaPlayer.shouldTriggerSubscribedTagEvent()) {
                                   // use timed metadata object
                               }
                           }
                       }
                   }
               }
           });
       }
   };
   _playbackClock.addClockEventListener(_playbackClockEventListener);
   ```

1. Svuotamento periodico non aggiornato `TimedMetadata` dall&#39;elenco per impedire che la memoria cresca continuamente.
