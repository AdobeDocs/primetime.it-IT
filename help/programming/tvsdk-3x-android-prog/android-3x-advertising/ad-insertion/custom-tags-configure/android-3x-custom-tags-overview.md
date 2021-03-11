---
title: Esempio di risorsa VOD personalizzata
description: Esempio di risorsa VOD personalizzata
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# Esempio di risorsa VOD personalizzata{#example-of-a-customized-vod-asset}

Ecco un esempio di risorsa VOD personalizzata:

```
#EXTM3U
#EXT-X-VERSION:3
#EXT-X-TARGETDURATION:7
 
#EXT-X-ASSET:AID=10
 
#EXTINF:9.9766,
seg1.ts
 
#EXTINF:9.9766,
seg2.ts
 
#EXTINF:9.9766,
seg3.ts
 
#EXT-X-AD:DURATION=10
#EXTINF:9.9766,
seg4.ts
 
#EXTINF:9.9766,
seg5.ts
 
#EXT-X-ENDLIST
```

L&#39;applicazione potrebbe configurare i seguenti scenari:

* Nel file è presente una notifica quando sono presenti tag `#EXT-X-ASSET` o qualsiasi altro set di nomi di tag personalizzati a cui hai effettuato la sottoscrizione.
* Inserisci annunci quando nel flusso è presente un tag `#EXT-X-AD` o qualsiasi altro nome di tag personalizzato.

