---
description: I flussi HLS che vengono consegnati tramite una rete CDN (Content Delivery Network) possono talvolta utilizzare token di autenticazione nelle richieste di verifica del manifesto e del segmento. Questi token possono essere forniti come parametri URL o come intestazioni dei cookie.
title: Flussi di segmenti token
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Flussi di segmenti token {#tokenized-segment-streams}

I flussi HLS che vengono consegnati tramite una rete CDN (Content Delivery Network) possono talvolta utilizzare token di autenticazione nelle richieste di verifica del manifesto e del segmento. Questi token possono essere forniti come parametri URL o come intestazioni dei cookie.

I token forniti come cookie nella risposta del manifesto master (m3u8) non sono condivisi con le richieste del segmento (ts) anche quando le richieste del segmento sono per lo stesso dominio. Per abilitare la condivisione di questi cookie in una richiesta di segmento, imposta la seguente proprietà sull&#39;istanza `PTMetadata` fornita all&#39;elemento del lettore: 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

Viene effettuata una richiesta aggiuntiva al manifesto principale (m3u8) prima che inizi la riproduzione del flusso.

>[!IMPORTANT]
>
>Questa funzione di condivisione dei cookie è supportata solo sui dispositivi con iOS 8 o versioni successive.

