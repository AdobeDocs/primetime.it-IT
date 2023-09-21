---
description: Puoi scegliere di utilizzare i comportamenti di annuncio predefiniti.
title: Utilizza il comportamento di riproduzione predefinito
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# Utilizza il comportamento di riproduzione predefinito {#use-the-default-playback-behavior}

Puoi scegliere di utilizzare i comportamenti di annuncio predefiniti.

1. Per utilizzare i comportamenti predefiniti, completa una delle seguenti attività:

   * Se implementi un `AdvertisingFactory` class, restituisce null per `createAdPolicySelector`.

   * Se non hai un’implementazione personalizzata per `AdvertisingFactory` classe, TVSDK utilizza un selettore di criteri di annunci predefinito.

## Impostare la riproduzione personalizzata {#set-up-customized-playback}

Puoi personalizzare o ignorare i comportamenti degli annunci.

Prima di poter personalizzare o ignorare i comportamenti degli annunci, registra l’istanza dei criteri degli annunci con .
Per personalizzare i comportamenti degli annunci, effettuare una delle seguenti operazioni:

* Implementare `AdPolicySelector` e tutti i relativi metodi.

  Questa opzione è consigliata se devi eseguire l’override di **tutto** i comportamenti di annuncio predefiniti.

* Estendi il `DefaultAdPolicySelector` e forniscono implementazioni solo per i comportamenti che richiedono personalizzazione.

  Questa opzione è consigliata solo se è necessario eseguire l&#39;override **alcuni** dei comportamenti predefiniti.

Per personalizzare i comportamenti degli annunci:

1. Implementare `AdPolicySelector` e tutti i relativi metodi.
1. Assegna l’istanza dei criteri che deve essere utilizzata da TVSDK tramite la advertising factory.

   >[!NOTE]
   >
   >la classe CustomContentFactory estende ContentFactory &amp;Locace;
   >...
   >@Override
   >public AdPolicySelector retrieveAdPolicySelector>>(MediaPlayerItem mediaPlayerItem) &amp;lbrace;
   >restituisce un nuovo elemento CustomAdPolicySelector(mediaPlayerItem);
   >&amp;parentesi graffa
   >...
   >&amp;parentesi graffa
   >// registrare la fabbrica di contenuti personalizzati con il lettore multimediale
   >Configurazione MediaPlayerItemConfig = new MediaPlayerItemConfig();
   >config.setAdvertisingFactory(new CustomContentFactory());
   >// questa configurazione dovrà essere passata in seguito durante il caricamento >della risorsa
   >mediaPlayer.replaceCurrentResource(resource, config);

1. Implementare le personalizzazioni.
