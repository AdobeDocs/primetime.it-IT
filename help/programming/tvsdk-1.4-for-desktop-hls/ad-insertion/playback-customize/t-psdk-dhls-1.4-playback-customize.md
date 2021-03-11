---
description: Puoi personalizzare o ignorare i comportamenti degli annunci.
title: Impostare una riproduzione personalizzata
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Imposta riproduzione personalizzata{#set-up-customized-playback}

Puoi personalizzare o ignorare i comportamenti degli annunci.

Prima di personalizzare o ignorare i comportamenti degli annunci, registra l’istanza del criterio degli annunci con .
Per personalizzare i comportamenti degli annunci, effettua una delle seguenti operazioni:

* Implementa l’interfaccia `AdPolicySelector` e tutti i relativi metodi.

   Questa opzione è consigliata se devi sovrascrivere **all** i comportamenti di annunci predefiniti.

* Estendi la classe `DefaultAdPolicySelector` e fornisci implementazioni solo per quei comportamenti che richiedono personalizzazione.

   Questa opzione è consigliata se è necessario ignorare solo **alcuni** dei comportamenti predefiniti.

Per entrambe le opzioni, completa le attività seguenti:

1. Implementa il tuo selettore di criteri per gli annunci personalizzati.

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. Estendi la content factory per utilizzare il selettore dei criteri per gli annunci personalizzati.

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

1. Registra il nuovo content factory che deve essere utilizzato da TVSDK nel flusso di lavoro pubblicitario.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >Se la content factory personalizzata è stata registrata per un flusso specifico attraverso la classe `MediaPlayerItemConfig`, verrà cancellata quando l&#39;istanza `MediaPlayer` viene deallocata. L&#39;applicazione deve registrarla ogni volta che viene creata una nuova sessione di riproduzione.