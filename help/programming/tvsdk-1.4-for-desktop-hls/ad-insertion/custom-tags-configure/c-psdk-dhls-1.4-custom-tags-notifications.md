---
description: La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 all'interno del flusso multimediale. La proprietà MediaPlayerItem.hasTimedMetadata indica se nel file multimediale corrente è presente un tag personalizzato con sottoscrizione.
title: Notifiche per i tag manifest
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Notifiche per i tag manifest{#notifications-for-manifest-tags}

La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 all&#39;interno del flusso multimediale. La proprietà MediaPlayerItem.hasTimedMetadata indica se nel file multimediale corrente è presente un tag personalizzato con sottoscrizione.

Puoi monitorare i metadati temporizzati ascoltando i seguenti eventi, che notificano all’applicazione le relative attività:

* `MediaPlayerItemEvent.ITEM_CREATED`: L’elenco iniziale di  `TimedMetadata` oggetti è disponibile dopo la creazione  `MediaPlayerItem` di . Questo evento notifica l&#39;applicazione quando si verifica questa situazione.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Per i flussi in diretta/lineare in cui il manifesto/playlist si aggiorna periodicamente, potrebbero essere visualizzati tag personalizzati aggiuntivi nella playlist/manifesto aggiornato, pertanto è possibile aggiungere alla  `MediaPlayerItem.timedMetadata` proprietà ulteriori oggetti TimedMetadata. Questo evento notifica l&#39;applicazione quando si verifica questa situazione.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Ogni volta che viene creato un nuovo  `TimedMetadata` oggetto, questo evento viene inviato da  `MediaPlayer`. Questo evento non viene inviato per l&#39;oggetto `TimedMetadata` creato durante la fase di inizializzazione.

