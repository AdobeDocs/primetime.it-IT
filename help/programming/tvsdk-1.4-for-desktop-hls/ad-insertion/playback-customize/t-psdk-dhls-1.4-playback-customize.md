---
description: Potete personalizzare o ignorare i comportamenti degli annunci.
seo-description: Potete personalizzare o ignorare i comportamenti degli annunci.
seo-title: Configurare la riproduzione personalizzata
title: Configurare la riproduzione personalizzata
uuid: 479ca1b0-6b3f-42fa-85e1-31d707da8730
translation-type: tm+mt
source-git-commit: a21a5fcc819a7bec58ad36e118d04f462ec3fd92
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Configurare la riproduzione personalizzata{#set-up-customized-playback}

Potete personalizzare o ignorare i comportamenti degli annunci.

Prima di poter personalizzare o ignorare i comportamenti degli annunci, registra l&#39;istanza dei criteri degli annunci con .
Per personalizzare i comportamenti degli annunci, effettuate una delle seguenti operazioni:

* Implementare l&#39;interfaccia `AdPolicySelector` e tutti i relativi metodi.

   Questa opzione è consigliata se dovete ignorare **all** i comportamenti annunci predefiniti.

* Estendete la classe `DefaultAdPolicySelector` e fornite implementazioni solo per quei comportamenti che richiedono la personalizzazione.

   Questa opzione è consigliata se è necessario ignorare solo **alcuni** dei comportamenti predefiniti.

Per entrambe le opzioni, completare le seguenti attività:

1. Implementa il selettore di criteri per gli annunci personalizzato.

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. Estendete la content factory per utilizzare il selettore di criteri per gli annunci personalizzato.

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       /** 
        * @inheritDoc 
        */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
           return new CustomAdPolicySelector(item); 
       } 
   }
   ```

   ```
   psdkutils::PSDKSharedPointer<psdk::ContentFactory> factory; 
   psdkFactory->createDefaultContentFactory(&factory); 
   psdkutils::PSDKSharedPointer<psdk::AdPolicySelector> defaultAdPolicySelector; 
   factory->retrieveAdPolicySelector(item, &defaultAdPolicySelector);
   ```

1. Registra il nuovo content factory da utilizzare per TVSDK nel flusso di lavoro della pubblicità.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >Se il content factory personalizzato è stato registrato per un flusso specifico attraverso la classe `MediaPlayerItemConfig`, verrà cancellato quando l&#39;istanza `MediaPlayer` viene deallocata. L’applicazione deve registrarla ogni volta che viene creata una nuova sessione di riproduzione.