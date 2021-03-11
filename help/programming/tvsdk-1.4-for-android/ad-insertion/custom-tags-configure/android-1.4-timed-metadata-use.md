---
description: È possibile utilizzare TimedMetadata quando il tempo di riproduzione corrente corrisponde all'ora di inizio.
title: Utilizzare i metadati temporizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 1%

---


# Utilizzare i metadati temporizzati {#use-timed-metadata}

È possibile utilizzare TimedMetadata quando il tempo di riproduzione corrente corrisponde all&#39;ora di inizio.

Per utilizzare questi oggetti salvati `TimedMetadata` durante la riproduzione, utilizzare i `ArrayList` salvati da [Memorizzare gli oggetti con metadati temporizzati durante l&#39;invio](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. Eseguire un timer ed eseguire ripetutamente una query sul tempo di riproduzione corrente.
1. Trova tutti gli oggetti `TimedMetadata` con tempi di avvio corrispondenti al tempo di riproduzione corrente.

   È possibile utilizzare questi oggetti per completare varie azioni.

   >[!IMPORTANT]
   >
   >Quando si controlla se il tempo di riproduzione corrente corrisponde a qualsiasi oggetto `TimedMetadata`, includere `shouldTriggerSubscribedTagEvent` come condizione.

   La timeline potrebbe cambiare come risultato di vari comportamenti di annunci. Ad esempio, una o più interruzioni pubblicitarie potrebbero essere spostate dalle posizioni originali nella timeline, ma `shouldTriggerSubscribedTagEvent` assicura che l&#39;ora di inizio dell&#39;oggetto `TimeMetadata` corrisponda al tempo di riproduzione corrente.

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

1. Svuotare periodicamente le istanze obsolete `TimedMetadata` dall&#39;elenco per evitare che la memoria cresca continuamente.