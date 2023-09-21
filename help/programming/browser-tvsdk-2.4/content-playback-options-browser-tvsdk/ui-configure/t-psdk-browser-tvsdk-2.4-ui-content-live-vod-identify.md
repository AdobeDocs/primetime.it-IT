---
description: Potrebbe essere necessario sapere se il contenuto multimediale è in diretta o VOD.
title: Identifica se il contenuto è live o VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
