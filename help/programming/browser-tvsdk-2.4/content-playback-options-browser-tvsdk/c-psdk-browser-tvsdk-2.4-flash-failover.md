---
description: Browser TVSDK fornisce strumenti per la creazione di un’applicazione per lettori video avanzata (il lettore Primetime), che potete integrare con altri componenti Primetime.
seo-description: Browser TVSDK fornisce strumenti per la creazione di un’applicazione per lettori video avanzata (il lettore Primetime), che potete integrare con altri componenti Primetime.
seo-title: 'null'
title: 'null'
uuid: 57b35a5f-87f8-41a2-ad85-300b999dc30b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Failover Flash {#flash-failover}

Browser TVSDK fornisce strumenti per la creazione di un’applicazione per lettori video avanzata (il lettore Primetime), che potete integrare con altri componenti Primetime.

Utilizzate gli strumenti della piattaforma per creare un lettore e collegarlo alla visualizzazione del lettore multimediale nel browser TVSDK, che dispone di metodi per riprodurre e gestire i video. Ad esempio, Browser TVSDK fornisce metodi di riproduzione e pausa. Potete creare pulsanti dell&#39;interfaccia utente sulla piattaforma e impostare i pulsanti per chiamare tali metodi del browser TVSDK.

## Flash fallback {#section_92D3884A13A6431F9A9CC5C79715D888}

In TVSDK browser, l&#39;applicazione interagisce solo con l&#39; `Primetime.js` API. L’implementazione TVSDK del browser sottostante determina quale tecnologia di lettore utilizzare in base alla piattaforma corrente e al tipo di risorsa del supporto da riprodurre.

La decisione per la tecnologia del lettore non viene presa finché non si chiama `MediaPlayer.replaceCurrentResource` a giocare una risorsa specifica.

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
>Il processo può variare a seconda dell’URL e dell’ambiente in uso.

1. Se le estensioni di origine multimediale sono supportate, utilizzatele senza limiti noti.
1. Se supportato, usate il `<video>` tag direttamente senza MSE.
1. Accertatevi di utilizzare almeno Adobe Flash Player versione 23.0.
1. Se non viene trovata alcuna tecnologia di riproduzione appropriata, `replaceCurrentResource` restituisce un errore.

Una `replaceCurrentResource` chiamata successiva alla stessa `MediaPlayer` istanza segue lo stesso processo. Questo consente di riprodurre vari tipi di risorse utilizzando la stessa `MediaPlayer` istanza nello stesso `<DIV>` tag principale specificato al momento della creazione dell&#39; `MediaPlayerView` istanza.

>[!TIP]
>
>L&#39;oggetto SWF e il `<video>` tag sono nidificati nel `<DIV>` tag principale.

