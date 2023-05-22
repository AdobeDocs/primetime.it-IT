---
description: Puoi personalizzare o ignorare i comportamenti degli annunci.
title: Impostare la riproduzione personalizzata
exl-id: aaa4d1c2-c425-4a2e-8377-0a3072f3fb18
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Configurazione della riproduzione personalizzata {#cset-up-customized-playback}

Puoi personalizzare o ignorare il comportamento degli annunci registrando l’istanza dei criteri degli annunci con TVSDK.

Per personalizzare i comportamenti degli annunci, effettuare una delle seguenti operazioni:

* Implementare `AdPolicySelector` e tutti i relativi metodi.
Questa opzione è consigliata se devi ignorare tutti i comportamenti di annuncio predefiniti.

* Estendi il `DefaultAdPolicySelector` e forniscono implementazioni solo per i comportamenti che richiedono personalizzazione.
Questa opzione è consigliata se devi ignorare solo alcuni dei comportamenti predefiniti.

Per entrambe le opzioni, completa le seguenti attività:

Per personalizzare i comportamenti degli annunci:

1. Implementare l&#39;interfaccia AdPolicySelector e tutti i relativi metodi.

1. Assegna l’istanza dei criteri che deve essere utilizzata da TVSDK tramite la advertising factory.

>[!IMPORTANT]
>
>I criteri degli annunci personalizzati registrati all’inizio della riproduzione vengono cancellati quando l’istanza MediaPlayer è deallocata. L’applicazione deve registrare un’istanza di criteri > selettore ogni volta che viene creata una nuova sessione di riproduzione.

Ad esempio:

```
    class CustomContentFactory extends ContentFactory {
     ...
    @Override
    public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) {
    return new CustomAdPolicySelector(mediaPlayerItem);
    }
     ...
    }
    TVSDK 1.4 for Android Programmer's Guide 46
    // register the custom content factory with media player
    MediaPlayerItemConfig config = new MediaPlayerItemConfig();
    config.setAdvertisingFactory(new CustomContentFactory());
    // this config will should be later passed while loading the resource
    mediaPlayer.replaceCurrentResource(resource, config);
```

1. Implementare le personalizzazioni.
