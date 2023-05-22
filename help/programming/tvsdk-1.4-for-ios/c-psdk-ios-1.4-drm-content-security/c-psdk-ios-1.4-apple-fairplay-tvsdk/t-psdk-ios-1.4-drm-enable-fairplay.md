---
description: Puoi implementare Apple FairPlay Streaming, la soluzione DRM di Apple, nelle applicazioni TVSDK.
title: Abilitare Apple FairPlay nelle applicazioni TVSDK
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Abilitare Apple FairPlay nelle applicazioni TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

Puoi implementare Apple FairPlay Streaming, la soluzione DRM di Apple, nelle applicazioni TVSDK.

1. Creare il programma FairPlay Customer Resource Loader implementando `PTAVAssetResourceLoaderDelegate`.

   Per ulteriori informazioni, consulta [Apple FairPlay nelle applicazioni TVSDK](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >Accertati di seguire le istruzioni riportate nella sezione *Guida al programma di streaming FairPlay* ( *FairPlayStreaming_PG.pdf*), incluso in [SDK del server FairPlay per lo sviluppo di un’app compatibile con FPS](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   Il `resourceLoader:shouldWaitForLoadingOfRequestedResource` il metodo equivale a quello in `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >Nello scenario del server di licenze ExpressPlay, per riprodurre il contenuto, modificare lo schema URL nell&#39;URL della richiesta di licenza del server ExpressPlay FairPlay da `skd://` a `https://` (o `https://`).

1. Registra il *FairPlay* Caricatore risorse cliente con `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Se si è creato il proprio server licenze FairPlay o si sta utilizzando un server licenze FairPlay di terze parti, consultare il fornitore del server licenze per determinare l&#39;URL del server licenze, la formattazione e altri requisiti.
