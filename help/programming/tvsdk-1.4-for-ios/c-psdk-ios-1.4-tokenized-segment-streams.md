---
description: I flussi HLS consegnati tramite una rete CDN (Content Delivery Network) possono a volte utilizzare token di autenticazione per le richieste di manifesto e segmento per la verifica. Questi token possono essere forniti come parametri URL o come intestazioni cookie.
title: Flussi di segmenti con token
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Flussi di segmenti con token{#tokenized-segment-streams}

I flussi HLS consegnati tramite una rete CDN (Content Delivery Network) possono a volte utilizzare token di autenticazione per le richieste di manifesto e segmento per la verifica. Questi token possono essere forniti come parametri URL o come intestazioni cookie.

I token forniti come cookie nella risposta del manifesto principale (m3u8) non sono condivisi con le richieste del segmento (ts) anche quando le richieste del segmento sono per lo stesso dominio. Per abilitare la condivisione di questi cookie in una richiesta di segmento, imposta la seguente proprietà su `PTMetadata` istanza fornita all’elemento del lettore: 

```
PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
[metadata setValue:[NSNumber numberWithBool:YES] forKey:kSyncCookiesWithAVAsset]; 
```

Viene effettuata una richiesta aggiuntiva al manifesto principale (m3u8) prima che il flusso inizi a essere riprodotto.

>[!IMPORTANT]
>
>Questa funzione di condivisione dei cookie è supportata solo sui dispositivi che eseguono iOS 8 o versioni successive.
