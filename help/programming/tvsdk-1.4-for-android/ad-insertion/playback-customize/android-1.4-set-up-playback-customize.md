---
description: Puoi personalizzare o ignorare i comportamenti degli annunci.
title: Impostare una riproduzione personalizzata
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 1%

---


# Configurare la riproduzione personalizzata {#cset-up-customized-playback}

Puoi personalizzare o sovrascrivere il comportamento degli annunci registrando l’istanza del criterio degli annunci con TVSDK.

Per personalizzare i comportamenti degli annunci, effettua una delle seguenti operazioni:

* Implementa l’interfaccia `AdPolicySelector` e tutti i relativi metodi.
Questa opzione è consigliata se devi sovrascrivere tutti i comportamenti di annunci predefiniti.

* Estendi la classe `DefaultAdPolicySelector` e fornisci implementazioni solo per quei comportamenti che richiedono
personalizzazione.
Questa opzione è consigliata se è necessario ignorare solo alcuni dei comportamenti predefiniti.

Per entrambe le opzioni, completa le attività seguenti:

Per personalizzare i comportamenti degli annunci:

1. Implementa l’interfaccia AdPolicySelector e tutti i relativi metodi.

1. Assegna l’istanza dei criteri che deve essere utilizzata da TVSDK tramite advertising factory.

>[!IMPORTANT]
>
>I criteri degli annunci personalizzati registrati all&#39;inizio di >playback vengono cancellati quando l&#39;istanza di MediaPlayer è >deallocate.L&#39;applicazione deve registrare un&#39;istanza di criterio >selettore ogni volta che viene creata una nuova sessione di riproduzione.

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

1. Implementa le tue personalizzazioni.