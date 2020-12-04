---
description: I flussi HLS inviati tramite una rete CDN (Content Delivery Network) possono talvolta utilizzare token di autenticazione per le richieste di verifica del manifesto e del segmento. Questi token possono essere forniti come parametri URL o come intestazioni di cookie.
seo-description: I flussi HLS inviati tramite una rete CDN (Content Delivery Network) possono talvolta utilizzare token di autenticazione per le richieste di verifica del manifesto e del segmento. Questi token possono essere forniti come parametri URL o come intestazioni di cookie.
seo-title: Flussi di segmenti con token
title: Flussi di segmenti con token
uuid: 62e3b858-2605-4960-b504-9010674f80ad
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Flussi di segmenti token {#tokenized-segment-streams}

I flussi HLS inviati tramite una rete CDN (Content Delivery Network) possono talvolta utilizzare token di autenticazione per le richieste di verifica del manifesto e del segmento. Questi token possono essere forniti come parametri URL o come intestazioni di cookie.

I token forniti come cookie nella risposta del manifesto master (m3u8) non vengono condivisi con le richieste del segmento (ts) anche quando le richieste del segmento sono per lo stesso dominio. Per abilitare la condivisione di questi cookie in una richiesta di segmento, imposta la seguente proprietà sull&#39;istanza `PTMetadata` fornita all&#39;elemento del lettore: 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

Una richiesta aggiuntiva viene fatta al manifesto master (m3u8) prima che inizi la riproduzione del flusso.

>[!IMPORTANT]
>
>Questa funzione di condivisione dei cookie è supportata solo sui dispositivi con iOS 8 o versione successiva.

