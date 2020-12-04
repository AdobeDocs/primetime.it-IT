---
description: Potete personalizzare o ignorare i comportamenti degli annunci.
seo-description: Potete personalizzare o ignorare i comportamenti degli annunci.
seo-title: Configurare la riproduzione personalizzata
title: Configurare la riproduzione personalizzata
uuid: 9cbf0bcf-7932-409e-a690-e79f284eaf74
translation-type: tm+mt
source-git-commit: 23a48208ac1d3625ae7d925ab6bfba8f2a980766
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---


# Configurare la riproduzione personalizzata {#cset-up-customized-playback}

Puoi personalizzare o ignorare il comportamento degli annunci registrando l&#39;istanza dei criteri degli annunci con TVSDK.

Per personalizzare i comportamenti degli annunci, effettuate una delle seguenti operazioni:

* Implementare l&#39;interfaccia `AdPolicySelector` e tutti i relativi metodi.
Questa opzione è consigliata se dovete sovrascrivere tutti i comportamenti di annunci predefiniti.

* Estendi la classe `DefaultAdPolicySelector` e fornisci implementazioni solo per quei comportamenti che richiedono
personalizzazione.
Questa opzione è consigliata se dovete ignorare solo alcuni dei comportamenti predefiniti.

Per entrambe le opzioni, completare le seguenti attività:

Per personalizzare i comportamenti degli annunci:

1. Implementa l’interfaccia AdPolicySelector e tutti i relativi metodi.

1. Assegnate l&#39;istanza del criterio che deve essere utilizzata da TVSDK tramite il modulo pubblicitario.

>[!IMPORTANT]
>
>I criteri di annunci personalizzati registrati all&#39;inizio di >riproduzione vengono cancellati quando l&#39;istanza di MediaPlayer è >deallocata. L&#39;applicazione deve registrare un&#39;istanza di criterio > selettore ogni volta che viene creata una nuova sessione di riproduzione.

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

1. Implementa le personalizzazioni.