---
description: Puoi scegliere di utilizzare i comportamenti annunci predefiniti.
seo-description: Puoi scegliere di utilizzare i comportamenti annunci predefiniti.
seo-title: Utilizzare il comportamento di riproduzione predefinito
title: Utilizzare il comportamento di riproduzione predefinito
uuid: 20785251-eb2f-4cc0-b919-1a88c0b1c57c
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---


# Utilizzare il comportamento di riproduzione predefinito {#use-the-default-playback-behavior}

Puoi scegliere di utilizzare i comportamenti annunci predefiniti.

1. Per utilizzare i comportamenti predefiniti, effettuare una delle seguenti operazioni:

   * Se implementate la vostra classe `AdvertisingFactory`, restituite null per `createAdPolicySelector`.

   * Se non disponete di un&#39;implementazione personalizzata per la classe `AdvertisingFactory`, TVSDK utilizza un selettore di criteri di annunci predefinito.

## Configurare la riproduzione personalizzata {#set-up-customized-playback}

Potete personalizzare o ignorare i comportamenti degli annunci.

Prima di personalizzare o ignorare i comportamenti degli annunci, registra l’istanza del criterio degli annunci con TVSDK.

* Implementare l&#39;interfaccia `AdPolicySelector` e tutti i relativi metodi.

   Questa opzione è consigliata se dovete ignorare **all** i comportamenti annunci predefiniti.

* Estendete la classe `DefaultAdPolicySelector` e fornite implementazioni solo per quei comportamenti che richiedono la personalizzazione.

   Questa opzione è consigliata se è necessario ignorare solo **alcuni** dei comportamenti predefiniti.

Per personalizzare i comportamenti degli annunci:

1. Implementare l&#39;interfaccia `AdPolicySelector` e tutti i relativi metodi.
1. Assegnate l&#39;istanza del criterio che deve essere utilizzata da TVSDK tramite il modulo pubblicitario.

   >[!NOTE]
   >
   >I criteri di annunci personalizzati registrati all&#39;inizio della riproduzione vengono cancellati quando l&#39;istanza `MediaPlayer` viene deallocata. L&#39;applicazione deve registrare un&#39;istanza del selettore criteri ogni volta che viene creata una nuova sessione di riproduzione.

   Ad esempio:

   ```java
   class CustomContentFactory extends ContentFactory { 
       ... 
       @Override 
       public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
           return new CustomAdPolicySelector(mediaPlayerItem); 
       } 
       ... 
   } 
   
   // register the custom content factory with media player 
   MediaPlayerItemConfig config =  new MediaPlayerItemConfig(); 
   config.setAdvertisingFactory(new CustomContentFactory()); 
   
   // this config will should be later passed while loading the resource 
   mediaPlayer.replaceCurrentResource(resource, config);
   ```

1. Implementa le personalizzazioni.