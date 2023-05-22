---
description: Per impostazione predefinita, all’avvio della riproduzione, il contenuto multimediale VOD inizia da 0 e il contenuto multimediale live inizia dal punto di attivazione del client (MediaPlayer.LIVE_POINT). È possibile ignorare il comportamento predefinito.
title: Immettere un flusso in un momento specifico
exl-id: 2fb361c1-7133-4e17-a12b-e11f6f7c5479
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Immettere un flusso in un momento specifico{#enter-a-stream-at-a-specific-time}

Per impostazione predefinita, all’avvio della riproduzione, il contenuto multimediale VOD inizia da 0 e il contenuto multimediale live inizia dal punto di attivazione del client (MediaPlayer.LIVE_POINT). È possibile ignorare il comportamento predefinito.

1. Passa una posizione a `MediaPlayer.prepareToPlay`.
1. Il TVSDK del browser utilizza questa posizione come punto di partenza per la risorsa.

   >[!NOTE]
   >
   >Non è richiesta alcuna operazione di ricerca.

1. Se la posizione non è compresa nell&#39;intervallo ricercabile, vengono utilizzate le posizioni di default.

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
