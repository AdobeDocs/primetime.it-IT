---
description: Per impostazione predefinita, all'avvio della riproduzione, il contenuto multimediale VOD inizia a 0 e il contenuto multimediale in tempo reale inizia dal punto live del client (MediaPlayer.LIVE_POINT). È possibile ignorare il comportamento predefinito.
title: Immettere un flusso in un momento specifico
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 1%

---


# Immettere un flusso in un momento specifico{#enter-a-stream-at-a-specific-time}

Per impostazione predefinita, all&#39;avvio della riproduzione, il contenuto multimediale VOD inizia a 0 e il contenuto multimediale in tempo reale inizia dal punto live del client (MediaPlayer.LIVE_POINT). È possibile ignorare il comportamento predefinito.

1. Passa una posizione a `MediaPlayer.prepareToPlay`.
1. Il browser TVSDK utilizza questa posizione come punto iniziale della risorsa.

   >[!NOTE]
   >
   >Non è richiesta alcuna operazione di ricerca.

1. Se la posizione non si trova all’interno dell’intervallo ricercabile, vengono utilizzate le posizioni predefinite.

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

