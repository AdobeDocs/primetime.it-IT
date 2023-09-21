---
description: La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 all'interno del flusso multimediale. La proprietà MediaPlayerItem.hasTimedMetadata indica se nel supporto corrente è presente un tag personalizzato sottoscritto.
title: Notifiche per i tag manifesto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Notifiche per i tag manifesto{#notifications-for-manifest-tags}

La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 all&#39;interno del flusso multimediale. La proprietà MediaPlayerItem.hasTimedMetadata indica se nel supporto corrente è presente un tag personalizzato sottoscritto.

Puoi monitorare i metadati temporizzati ascoltando i seguenti eventi, che notificano all’applicazione l’attività correlata:

* `MediaPlayerItemEvent.ITEM_CREATED`: elenco iniziale di `TimedMetadata` Gli oggetti sono disponibili dopo il `MediaPlayerItem` viene creato. Questo evento avvisa l&#39;applicazione quando si verifica.

* `MediaPlayerItemEvent.ITEM_UPDATED`: per i flussi live/lineari in cui il manifesto/la playlist viene aggiornato periodicamente, è possibile che nella playlist/il manifesto aggiornato vengano visualizzati tag personalizzati aggiuntivi, pertanto è possibile aggiungere al `MediaPlayerItem.timedMetadata` proprietà. Questo evento avvisa l&#39;applicazione quando si verifica.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: ogni volta che un nuovo `TimedMetadata` viene creato, questo evento viene inviato da `MediaPlayer`. Questo evento non viene inviato per `TimedMetadata` oggetto creato durante la fase di inizializzazione.
