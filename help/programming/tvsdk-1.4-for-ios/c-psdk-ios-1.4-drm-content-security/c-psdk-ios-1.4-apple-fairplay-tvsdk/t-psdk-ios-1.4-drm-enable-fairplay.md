---
description: Potete implementare Apple FairPlay Streaming, che è la soluzione DRM di Apple, nelle vostre applicazioni TVSDK.
seo-description: Potete implementare Apple FairPlay Streaming, che è la soluzione DRM di Apple, nelle vostre applicazioni TVSDK.
seo-title: Abilitare Apple FairPlay nelle applicazioni TVSDK
title: Abilitare Apple FairPlay nelle applicazioni TVSDK
uuid: fafffdb9-09f9-45fb-9957-3c6e95ed55f9
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Abilita Apple FairPlay nelle applicazioni TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

Potete implementare Apple FairPlay Streaming, che è la soluzione DRM di Apple, nelle vostre applicazioni TVSDK.

1. Crea il caricatore di risorse cliente FairPlay implementando `PTAVAssetResourceLoaderDelegate`.

   Per ulteriori informazioni, consultate [Apple FairPlay in applicazioni TVSDK](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >Assicurati di seguire le istruzioni riportate nella *Guida al programma di streaming FairPlay* ( *FairPlayStreaming_PG.pdf*), inclusa in [FairPlay Server SDK per lo sviluppo di un&#39;app in base a FPS](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   Il metodo `resourceLoader:shouldWaitForLoadingOfRequestedResource` equivale a quello presente in `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >Nello scenario del server licenze ExpressPlay, per riprodurre contenuto, modificate lo schema URL nell&#39;URL della richiesta di licenza del server ExpressPlay FairPlay da `skd://` a `https://` (o `https://`).

1. Registrare il caricatore di risorse cliente *FairPlay* con `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Se avete scritto il vostro server licenze FairPlay o state utilizzando un server licenze FairPlay di terze parti, consultate il fornitore del server licenze per determinare l’URL del server licenze, la formattazione e altri requisiti.
