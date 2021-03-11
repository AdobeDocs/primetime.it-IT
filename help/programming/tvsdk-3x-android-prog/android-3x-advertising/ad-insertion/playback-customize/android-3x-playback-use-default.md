---
description: Puoi scegliere di utilizzare i comportamenti degli annunci predefiniti.
title: Utilizzare il comportamento di riproduzione predefinito
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Utilizzare il comportamento di riproduzione predefinito {#use-the-default-playback-behavior}

Puoi scegliere di utilizzare i comportamenti degli annunci predefiniti.

1. Per utilizzare i comportamenti predefiniti, effettua una delle operazioni seguenti:

   * Se implementi la tua classe `AdvertisingFactory`, restituisce null per `createAdPolicySelector`.

   * Se non disponi di un’implementazione personalizzata per la classe `AdvertisingFactory` , TVSDK utilizza un selettore predefinito di criteri per gli annunci.

## Imposta riproduzione personalizzata {#set-up-customized-playback}

Puoi personalizzare o ignorare i comportamenti degli annunci.

Prima di personalizzare o ignorare i comportamenti degli annunci, registra l’istanza del criterio degli annunci con .
Per personalizzare i comportamenti degli annunci, effettua una delle seguenti operazioni:

* Implementa l’interfaccia `AdPolicySelector` e tutti i relativi metodi.

   Questa opzione è consigliata se devi sovrascrivere **all** i comportamenti di annunci predefiniti.

* Estendi la classe `DefaultAdPolicySelector` e fornisci implementazioni solo per quei comportamenti che richiedono personalizzazione.

   Questa opzione è consigliata se è necessario ignorare solo **alcuni** dei comportamenti predefiniti.

Per personalizzare i comportamenti degli annunci:

1. Implementa l&#39;interfaccia `AdPolicySelector` e tutti i relativi metodi.
1. Assegna l’istanza dei criteri che deve essere utilizzata da TVSDK tramite advertising factory.

   >[!NOTE]
   >
   >Classe CustomContentFactory estende ContentFactory &amp;lbrace;
   >...
   >@Override
   >pubblico AdPolicySelector retrieveAdPolicySelector>>>(MediaPlayerItem mediaPlayerItem) &amp;parentesi graffa;
   >restituisce il nuovo CustomAdPolicySelector(mediaPlayerItem);
   >&amp;parentesi graffa;
   >...
   >&amp;parentesi graffa;
   >// registra il content factory personalizzato con media player
   >File di configurazione MediaPlayerItemConfig = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// questa configurazione verrà successivamente trasmessa durante il caricamento >della risorsa
   >mediaPlayer.replaceCurrentResource(resource, config);

1. Implementa le tue personalizzazioni.
