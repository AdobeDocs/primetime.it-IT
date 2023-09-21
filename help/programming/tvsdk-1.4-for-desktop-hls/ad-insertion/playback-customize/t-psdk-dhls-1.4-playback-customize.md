---
description: Puoi personalizzare o ignorare i comportamenti degli annunci.
title: Impostare la riproduzione personalizzata
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Impostare la riproduzione personalizzata{#set-up-customized-playback}

Puoi personalizzare o ignorare i comportamenti degli annunci.

Prima di poter personalizzare o ignorare i comportamenti degli annunci, registra l’istanza dei criteri degli annunci con .
Per personalizzare i comportamenti degli annunci, effettuare una delle seguenti operazioni:

* Implementare `AdPolicySelector` e tutti i relativi metodi.

  Questa opzione è consigliata se devi eseguire l’override di **tutto** i comportamenti di annuncio predefiniti.

* Estendi il `DefaultAdPolicySelector` e forniscono implementazioni solo per i comportamenti che richiedono personalizzazione.

  Questa opzione è consigliata solo se è necessario eseguire l&#39;override **alcuni** dei comportamenti predefiniti.

Per entrambe le opzioni, completa le seguenti attività:

1. Implementa un selettore di criteri per gli annunci personalizzato.

   ```
   public class CustomAdPolicySelector implements AdPolicySelector { 
       // your own customization here 
   }
   ```

1. Estendi il factory dei contenuti per utilizzare il selettore dei criteri degli annunci personalizzati.

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

1. Registra la nuova fabbrica di contenuti che deve essere utilizzata da TVSDK nel flusso di lavoro per la pubblicità.

   ```
   PSDKConfig.advertisingFactory = new CustomContentFactory();
   ```

   >[!TIP]
   >
   >Se la content factory personalizzata è stata registrata per un flusso specifico tramite `MediaPlayerItemConfig` classe, verrà cancellato quando `MediaPlayer` istanza deallocata. L’applicazione deve registrarla ogni volta che viene creata una nuova sessione di riproduzione.
