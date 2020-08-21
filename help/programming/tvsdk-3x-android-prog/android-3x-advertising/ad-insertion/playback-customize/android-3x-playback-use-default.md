---
description: Puoi scegliere di utilizzare i comportamenti annunci predefiniti.
seo-description: Puoi scegliere di utilizzare i comportamenti annunci predefiniti.
seo-title: Utilizzare il comportamento di riproduzione predefinito
title: Utilizzare il comportamento di riproduzione predefinito
uuid: 36f76c42-4c6c-4620-9b47-ec97519a642a
translation-type: tm+mt
source-git-commit: 6da7d597503d98875735c54e9a794f8171ad408b
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Utilizzare il comportamento di riproduzione predefinito {#use-the-default-playback-behavior}

Puoi scegliere di utilizzare i comportamenti annunci predefiniti.

1. Per utilizzare i comportamenti predefiniti, effettuare una delle seguenti operazioni:

   * Se implementate la vostra `AdvertisingFactory` classe, restituite null per `createAdPolicySelector`.

   * Se non disponete di un&#39;implementazione personalizzata per la `AdvertisingFactory` classe, TVSDK utilizza un selettore di criteri di annunci predefinito.

## Configurare la riproduzione personalizzata {#set-up-customized-playback}

Potete personalizzare o ignorare i comportamenti degli annunci.

Prima di poter personalizzare o ignorare i comportamenti degli annunci, registra l&#39;istanza dei criteri degli annunci con .
Per personalizzare i comportamenti degli annunci, effettuate una delle seguenti operazioni:

* Implementare l&#39; `AdPolicySelector` interfaccia e tutti i relativi metodi.

   Questa opzione è consigliata se avete la necessità di ignorare **tutti** i comportamenti di annunci predefiniti.

* Estendete la `DefaultAdPolicySelector` classe e fornite implementazioni solo per quei comportamenti che richiedono la personalizzazione.

   Questa opzione è consigliata se dovete ignorare solo **alcuni** comportamenti predefiniti.

Per personalizzare i comportamenti degli annunci:

1. Implementare l&#39; `AdPolicySelector` interfaccia e tutti i relativi metodi.
1. Assegnate l&#39;istanza del criterio che deve essere utilizzata da TVSDK tramite il modulo pubblicitario.

   >[!NOTE]
   >
   >class CustomContentFactory estende ContentFactory &amp;lbrace;
   >...
   >@Override
   >public AdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem) &amp;lbrace;
   >restituisce il nuovo CustomAdPolicySelector(mediaPlayerItem);
   >&amp;rampa;
   >...
   >&amp;rampa;
   >// Registra il content factory personalizzato con il lettore multimediale
   >Configurazione MediaPlayerItemConfig = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// Questa configurazione verrà successivamente passata durante il caricamento > la risorsa
   >mediaPlayer.replaceCurrentResource(resource, config);

1. Implementa le personalizzazioni.
