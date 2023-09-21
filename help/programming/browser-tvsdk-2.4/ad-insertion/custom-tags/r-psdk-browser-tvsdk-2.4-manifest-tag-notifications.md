---
description: La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 nel flusso multimediale.
title: Notifiche per i tag manifesto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Notifiche per i tag manifesto{#notifications-for-manifest-tags}

La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 nel flusso multimediale.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

Il `MediaPlayerItem.hasTimedMetadata` indica se il supporto corrente contiene un tag personalizzato sottoscritto. È possibile monitorare i metadati temporizzati ascoltando `Events.TimedMetadataEvent`, che l’istanza MediaPlayer invia ogni volta che viene `TimedMetadata` viene creato l&#39;oggetto.
