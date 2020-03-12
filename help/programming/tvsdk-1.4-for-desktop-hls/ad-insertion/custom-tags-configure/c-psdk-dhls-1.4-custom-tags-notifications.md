---
description: La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 all'interno del flusso multimediale. La proprietà MediaPlayerItem.hasTimedMetadata indica se nel supporto corrente è presente un tag personalizzato con sottoscrizione.
seo-description: La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 all'interno del flusso multimediale. La proprietà MediaPlayerItem.hasTimedMetadata indica se nel supporto corrente è presente un tag personalizzato con sottoscrizione.
seo-title: Notifiche per i tag manifest
title: Notifiche per i tag manifest
uuid: 87bee41b-b44e-4d12-afd2-7a63023f992c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Notifiche per i tag manifest{#notifications-for-manifest-tags}

La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 all&#39;interno del flusso multimediale. La proprietà MediaPlayerItem.hasTimedMetadata indica se nel supporto corrente è presente un tag personalizzato con sottoscrizione.

Potete monitorare i metadati temporizzati ascoltando i seguenti eventi, che notificano all’applicazione le relative attività:

* `MediaPlayerItemEvent.ITEM_CREATED`: L&#39;elenco iniziale di `TimedMetadata` oggetti è disponibile dopo la creazione `MediaPlayerItem` . Questo evento notifica l’applicazione in caso di evento.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Per i flussi live/lineari in cui il manifest/playlist viene aggiornato periodicamente, è possibile che nella playlist/nel manifesto aggiornato vengano visualizzati tag personalizzati aggiuntivi, pertanto è possibile aggiungere alla `MediaPlayerItem.timedMetadata` proprietà ulteriori oggetti TimedMetadata. Questo evento notifica l’applicazione in caso di evento.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Ogni volta che viene creato un nuovo `TimedMetadata` oggetto, questo evento viene inviato dall&#39; `MediaPlayer`. Questo evento non viene inviato per l&#39; `TimedMetadata` oggetto creato durante la fase di inizializzazione.

