---
description: Potrebbe essere necessario sapere se il contenuto multimediale è in diretta o VOD.
title: Identifica se il contenuto è live o VOD
exl-id: fb15c779-db25-4858-b7d7-ae5eabf646a3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# Identifica se il contenuto è live o VOD{#identify-whether-the-content-is-live-or-vod}

Potrebbe essere necessario sapere se il contenuto multimediale è in diretta o VOD.

1. Attendere che TVSDK del browser attivi un `AdobePSDK.PSDKEventType.STATUS_CHANGED` evento con un `event.status` di `AdobePSDK.MediaPlayerStatus.PREPARED`.

   Questo passaggio assicura che la risorsa multimediale sia stata caricata correttamente.

   >[!IMPORTANT]
   >
   >Se il TVSDK del browser non si trova almeno nel `PREPARED` stato, il tentativo di chiamare i seguenti metodi genera un `IllegalStateException`.

1. Letto `live` dal `MediaPlayerItem` Interfaccia:

   ```js
   player.currentItem.live
   ```
