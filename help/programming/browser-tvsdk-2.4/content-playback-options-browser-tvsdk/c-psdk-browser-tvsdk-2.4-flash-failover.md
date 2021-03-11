---
description: Il browser TVSDK fornisce strumenti per la creazione di un’applicazione di lettore video avanzata (il lettore Primetime), che puoi integrare con altri componenti Primetime.
title: Failover Flash
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# Failover Flash {#flash-failover}

Il browser TVSDK fornisce strumenti per la creazione di un’applicazione di lettore video avanzata (il lettore Primetime), che puoi integrare con altri componenti Primetime.

Utilizza gli strumenti della piattaforma per creare un lettore e collegarlo alla visualizzazione del lettore multimediale nel browser TVSDK, che dispone di metodi per riprodurre e gestire i video. Ad esempio, il browser TVSDK fornisce metodi di riproduzione e pausa. Puoi creare pulsanti dell’interfaccia utente sulla piattaforma e impostare i pulsanti per chiamare tali metodi del browser TVSDK.

## Flash fallback {#section_92D3884A13A6431F9A9CC5C79715D888}

Nel browser TVSDK, l&#39;applicazione interagisce solo con l&#39; `Primetime.js` API. L’implementazione TVSDK del browser sottostante determina la tecnologia del lettore da utilizzare in base alla piattaforma corrente e al tipo di risorsa del supporto da riprodurre.

La decisione relativa alla tecnologia del lettore viene presa solo dopo aver chiamato `MediaPlayer.replaceCurrentResource` per riprodurre una risorsa specifica.

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

1. Se è supportato, utilizzalo senza limitazioni note.
1. Se supportato, utilizza il tag `<video>` direttamente senza MSE.
1. Assicurati di utilizzare almeno la versione 23.0 di Adobe Flash Player.
1. Se non viene trovata alcuna tecnologia di riproduzione adatta, `replaceCurrentResource` restituisce un errore.

Una successiva chiamata `replaceCurrentResource` sulla stessa istanza `MediaPlayer` segue lo stesso processo. Questo consente di riprodurre vari tipi di risorse utilizzando la stessa istanza `MediaPlayer` nello stesso tag `<DIV>` padre specificato al momento della creazione dell&#39;istanza `MediaPlayerView`.

>[!TIP]
>
>L&#39;oggetto SWF e il tag `<video>` sono nidificati nel tag `<DIV>` principale.

