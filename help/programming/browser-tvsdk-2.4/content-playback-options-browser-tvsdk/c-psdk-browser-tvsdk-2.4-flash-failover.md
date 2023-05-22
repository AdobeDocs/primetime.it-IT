---
description: Il browser TVSDK fornisce gli strumenti per creare un’applicazione video player avanzata (il lettore Primetime), che puoi integrare con altri componenti di Primetime.
title: Failover del Flash
exl-id: 76bd9214-767a-4f26-977d-81fbac3e0c42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Failover del Flash {#flash-failover}

Il browser TVSDK fornisce gli strumenti per creare un’applicazione video player avanzata (il lettore Primetime), che puoi integrare con altri componenti di Primetime.

Utilizza gli strumenti della tua piattaforma per creare un lettore e collegarlo alla visualizzazione del lettore multimediale in Browser TVSDK, che dispone di metodi per riprodurre e gestire i video. Ad esempio, Browser TVSDK fornisce metodi di riproduzione e pausa. Puoi creare pulsanti dell’interfaccia utente sulla tua piattaforma e impostarli per chiamare tali metodi TVSDK del browser.

## Fallback Flash {#section_92D3884A13A6431F9A9CC5C79715D888}

In Browser TVSDK, l’applicazione interagisce solo con `Primetime.js` API. L’implementazione Browser TVSDK sottostante determina la tecnologia del lettore da utilizzare in base alla piattaforma corrente e al tipo di risorsa del file multimediale da riprodurre.

La decisione per la tecnologia del lettore non viene presa fino a quando non chiami `MediaPlayer.replaceCurrentResource` per riprodurre una risorsa specifica.

Ad esempio:

```js
var player = new AdobePSDK.MediaPlayer(), 
              mediaResource = new AdobePSDK.MediaResource(url, 
              AdobePSDK.MediaResource.Type.TYPE_HLS); 
              ... 
              player.replaceCurrentResource(mediaResource);
```

## Determinare il lettore multimediale da utilizzare {#section_D844E386AF5848688D204DEE258ECEE6}

Questa procedura di esempio illustra il processo di determinazione della tecnologia del lettore:

>[!TIP]
>
>Il processo può variare a seconda dell’URL e dell’ambiente.

1. Se sono supportate le estensioni dell’origine multimediale, utilizzale senza limitazioni note.
1. Se supportato, utilizza `<video>` direttamente senza MSE.
1. Assicurati di utilizzare almeno la versione 23.0 del Flash Player Adobe.
1. Se non viene trovata alcuna tecnologia di riproduzione adatta, `replaceCurrentResource` restituisce un errore.

Una successiva `replaceCurrentResource` invoca lo stesso `MediaPlayer` segue lo stesso processo. Questo consente di riprodurre vari tipi di risorse utilizzando lo stesso `MediaPlayer` istanza nello stesso elemento padre `<DIV>` che hai specificato quando `MediaPlayerView` istanza creata.

>[!TIP]
>
>L&#39;oggetto SWF e `<video>` i tag sono nidificati nell&#39;elemento padre `<DIV>` tag.
