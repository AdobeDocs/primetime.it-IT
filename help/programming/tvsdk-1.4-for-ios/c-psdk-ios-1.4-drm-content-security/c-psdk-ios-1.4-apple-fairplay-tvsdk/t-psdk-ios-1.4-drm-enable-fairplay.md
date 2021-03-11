---
description: È possibile implementare Apple FairPlay Streaming, che è la soluzione DRM di Apple, nelle applicazioni TVSDK.
title: Abilitare Apple FairPlay nelle applicazioni TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Abilita Apple FairPlay nelle applicazioni TVSDK{#enable-apple-fairplay-in-tvsdk-applications}

È possibile implementare Apple FairPlay Streaming, che è la soluzione DRM di Apple, nelle applicazioni TVSDK.

1. Crea il tuo programma di caricamento risorse del cliente FairPlay implementando `PTAVAssetResourceLoaderDelegate`.

   Per ulteriori informazioni, consulta [Apple FairPlay nelle applicazioni TVSDK](../../c-psdk-ios-1.4-drm-content-security/c-psdk-ios-1.4-apple-fairplay-tvsdk/c-psdk-ios-1.4-apple-fairplay-tvsdk.md).

   >[!NOTE]
   >
   >Assicurati di seguire le istruzioni contenute nella *Guida al programma FairPlay Streaming* ( *FairPlayStreaming_PG.pdf*), inclusa in [FairPlay Server SDK per lo sviluppo di un&#39;app FPS-Aware](https://developer.apple.com/services-account/download?path=/Developer_Tools/FairPlay_Streaming_SDK/FairPlay_Streaming_Server_SDK.zip)).

   Il metodo `resourceLoader:shouldWaitForLoadingOfRequestedResource` equivale a quello in `AVAssetResourceLoaderDelegate`.

   >[!IMPORTANT]
   >
   >Nello scenario del server licenze ExpressPlay, per riprodurre il contenuto, modifica lo schema URL nell’URL della richiesta di licenza del server ExpressPlay FairPlay da `skd://` a `https://` (o `https://`).

1. Registra il *FairPlay* Customer Resource Loader con `registerPTAVAssetResourceLoader`.

   ```
   PTFairPlayResourceLoader *resourceLoader =  
     [[PTFairPlayResourceLoader new] autorelease];  
   [[PTDefaultMediaPlayerClientFactory defaultFactory]  
     registerPTAVAssetResourceLoader:resourceLoader];
   ```

Se hai scritto il tuo server licenze FairPlay o stai utilizzando un server licenze FairPlay di terze parti, consulta il fornitore del server licenze per determinare l&#39;URL del server licenze, la formattazione e altri requisiti.
