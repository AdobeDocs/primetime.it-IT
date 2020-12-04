---
description: Per impostazione predefinita, all’avvio della riproduzione, il supporto VOD inizia a 0 e il supporto live inizia dal punto di vista del client (MediaPlayer.LIVE_POINT). Potete ignorare il comportamento predefinito.
seo-description: Per impostazione predefinita, all’avvio della riproduzione, il supporto VOD inizia a 0 e il supporto live inizia dal punto di vista del client (MediaPlayer.LIVE_POINT). Potete ignorare il comportamento predefinito.
seo-title: Inserire un flusso in un momento specifico
title: Inserire un flusso in un momento specifico
uuid: 5db73b50-0629-4fb1-8f12-6c88e4cd7109
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 1%

---


# Immettere un flusso in un momento specifico{#enter-a-stream-at-a-specific-time}

Per impostazione predefinita, all’avvio della riproduzione, il supporto VOD inizia a 0 e il supporto live inizia dal punto di vista del client (MediaPlayer.LIVE_POINT). Potete ignorare il comportamento predefinito.

1. Passa una posizione a `MediaPlayer.prepareToPlay`.
1. Il browser TVSDK utilizza questa posizione come punto di partenza per la risorsa.

   >[!NOTE]
   >
   >Non è richiesta alcuna operazione di ricerca.

1. Se la posizione non è all’interno dell’intervallo ricercabile, vengono utilizzate le posizioni predefinite.

   Ad esempio:

   ```js
   var desiredPostion = //choose a value; 
   onStatusChange = function (event) { 
       case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
           console.log("Player Status: INITIALIZED"); 
           player.prepareToPlay(desiredPostion); 
           break; 
   } 
   ```

