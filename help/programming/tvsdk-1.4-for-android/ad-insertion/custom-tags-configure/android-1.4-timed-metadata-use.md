---
description: Potete usare TimedMetadata quando l’ora di riproduzione corrente corrisponde all’ora di inizio.
seo-description: Potete usare TimedMetadata quando l’ora di riproduzione corrente corrisponde all’ora di inizio.
seo-title: Utilizzare i metadati temporizzati
title: Utilizzare i metadati temporizzati
uuid: 98bb8c08-2794-42d6-b5c3-b1047ac804fe
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---


# Utilizzare i metadati temporizzati {#use-timed-metadata}

Potete usare TimedMetadata quando l’ora di riproduzione corrente corrisponde all’ora di inizio.

Per utilizzare questi oggetti `TimedMetadata` salvati durante la riproduzione, utilizzare gli oggetti `ArrayList` salvati da [Memorizzare gli oggetti con metadati temporizzati durante l&#39;invio](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. Eseguire un timer ed eseguire ripetutamente una query sul tempo di riproduzione corrente.
1. Trovate tutti gli oggetti `TimedMetadata` con orari di inizio che corrispondano al tempo di riproduzione corrente.

   È possibile utilizzare questi oggetti per completare diverse azioni.

   >[!IMPORTANT]
   >
   >Quando si verifica che il tempo di riproduzione corrente corrisponda a qualsiasi oggetto `TimedMetadata`, includere `shouldTriggerSubscribedTagEvent` come condizione.

   La timeline potrebbe cambiare a seguito di vari comportamenti di annunci. Ad esempio, una o più interruzioni pubblicitarie potrebbero essere spostate dalle posizioni originali nella timeline, ma `shouldTriggerSubscribedTagEvent` garantisce che l&#39;ora di inizio dell&#39;oggetto `TimeMetadata` corrisponda al tempo di riproduzione corrente.

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

1. Svuotare periodicamente le istanze `TimedMetadata` stantate dall&#39;elenco per evitare la crescita continua della memoria.