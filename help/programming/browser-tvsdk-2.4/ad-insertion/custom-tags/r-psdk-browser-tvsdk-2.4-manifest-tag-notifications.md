---
description: La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 nel flusso multimediale.
seo-description: La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 nel flusso multimediale.
seo-title: Notifiche per i tag manifest
title: Notifiche per i tag manifest
uuid: 50727455-b37b-4e39-8efb-a97de3164074
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Notifiche per i tag manifest{#notifications-for-manifest-tags}

La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 nel flusso multimediale.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

La proprietà `MediaPlayerItem.hasTimedMetadata` indica se nel supporto corrente esiste un tag personalizzato con sottoscrizione. È possibile monitorare i metadati temporizzati ascoltando il `Events.TimedMetadataEvent`, che l&#39;istanza MediaPlayer invia ogni volta che viene creato un nuovo oggetto `TimedMetadata`.
