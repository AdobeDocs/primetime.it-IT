---
description: La proprietà MediaPlayerItem.timedMetadata fornisce l'accesso a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 nel flusso multimediale.
title: Notifiche per i tag manifest
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Notifiche per i tag manifest{#notifications-for-manifest-tags}

La proprietà MediaPlayerItem.timedMetadata fornisce l&#39;accesso a tutti gli oggetti TimedMetadata creati dai tag playlist/manifest o dai tag ID3 nel flusso multimediale.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

La proprietà `MediaPlayerItem.hasTimedMetadata` indica se nel file multimediale corrente esiste un tag personalizzato sottoscritto. È possibile monitorare i metadati temporizzati ascoltando il `Events.TimedMetadataEvent`, che l&#39;istanza MediaPlayer invia ogni volta che viene creato un nuovo oggetto `TimedMetadata`.
