---
description: Potete implementare Apple FairPlay Streaming, che è la soluzione DRM di Apple, nelle vostre applicazioni TVSDK.
seo-description: Potete implementare Apple FairPlay Streaming, che è la soluzione DRM di Apple, nelle vostre applicazioni TVSDK.
seo-title: Abilitare Apple FairPlay nelle applicazioni TVSDK
title: Abilitare Apple FairPlay nelle applicazioni TVSDK
uuid: fafffdb9-09f9-45fb-9957-3c6e95ed55f9
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Abilitare Apple FairPlay nelle applicazioni TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

Potete implementare Apple FairPlay Streaming, che è la soluzione DRM di Apple, nelle vostre applicazioni TVSDK.

1. Crea il caricatore di risorse cliente FairPlay implementando `PTAVAssetResourceLoaderDelegate`.

   Per ulteriori informazioni, consultate [Apple FairPlay nelle applicazioni](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md)TVSDK.

   >[!NOTE]
   >
   >Accertatevi di seguire le istruzioni riportate nella guida *al programma* FairPlay Streaming ( *FairPlayStreaming_PG.pdf*), inclusa nell’SDK per server [FairPlay per lo sviluppo di un’app](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)in base a FPS.

   Il `resourceLoader:shouldWaitForLoadingOfRequestedResource` metodo è equivalente a quello presente in `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT] {important=&quot;high&quot;}
   >
   >Nello scenario del server licenze ExpressPlay, per riprodurre contenuto, modificate lo schema URL nell’URL della richiesta di licenza del server ExpressPlay FairPlay da `skd://` a `https://` (o `https://`).

1. Registra il caricatore di risorse cliente *FairPlay* con `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Se avete scritto il vostro server licenze FairPlay o state utilizzando un server licenze FairPlay di terze parti, consultate il fornitore del server licenze per determinare l’URL del server licenze, la formattazione e altri requisiti.
