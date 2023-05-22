---
description: La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 nel flusso multimediale.
title: Notifiche per i tag manifesto
exl-id: a8a3cada-d796-460a-bd8f-fc4a2703e7f0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Notifiche per i tag manifesto{#notifications-for-manifest-tags}

La proprietà MediaPlayerItem.timedMetadata consente di accedere a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 nel flusso multimediale.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

Il `MediaPlayerItem.hasTimedMetadata` indica se il supporto corrente contiene un tag personalizzato sottoscritto. È possibile monitorare i metadati temporizzati ascoltando `Events.TimedMetadataEvent`, che l’istanza MediaPlayer invia ogni volta che viene `TimedMetadata` viene creato l&#39;oggetto.
