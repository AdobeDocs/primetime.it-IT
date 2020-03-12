---
description: I flussi HLS inviati tramite una rete CDN (Content Delivery Network) possono talvolta utilizzare token di autenticazione per le richieste di verifica del manifesto e del segmento. Questi token possono essere forniti come parametri URL o come intestazioni di cookie.
seo-description: I flussi HLS inviati tramite una rete CDN (Content Delivery Network) possono talvolta utilizzare token di autenticazione per le richieste di verifica del manifesto e del segmento. Questi token possono essere forniti come parametri URL o come intestazioni di cookie.
seo-title: Flussi di segmenti con token
title: Flussi di segmenti con token
uuid: b17bb5bc-2029-4113-ac44-b1d30aa08ca6
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Flussi di segmenti con token{#tokenized-segment-streams}

I flussi HLS inviati tramite una rete CDN (Content Delivery Network) possono talvolta utilizzare token di autenticazione per le richieste di verifica del manifesto e del segmento. Questi token possono essere forniti come parametri URL o come intestazioni di cookie.

I token forniti come cookie nella risposta del manifesto master (m3u8) non vengono condivisi con le richieste del segmento (ts) anche quando le richieste del segmento sono per lo stesso dominio. Per abilitare la condivisione di questi cookie in una richiesta di segmento, imposta la seguente proprietà sull’ `PTMetadata` istanza fornita all’elemento del lettore:

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

Una richiesta aggiuntiva viene fatta al manifesto master (m3u8) prima che inizi la riproduzione del flusso.

>[!IMPORTANT]
>
>Questa funzione di condivisione dei cookie è supportata solo sui dispositivi con iOS 8 o versione successiva.

