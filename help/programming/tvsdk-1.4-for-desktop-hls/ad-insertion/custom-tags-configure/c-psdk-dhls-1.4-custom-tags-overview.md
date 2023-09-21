---
title: Esempio di risorsa VOD personalizzata
description: Esempio di risorsa VOD personalizzata
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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

L&#39;applicazione può configurare i seguenti scenari:

* Una notifica quando `#EXT-X-ASSET` I tag, o qualsiasi altro insieme di nomi di tag personalizzati a cui ti sei iscritto, sono già presenti nel file.
* Inserisci annunci quando un `#EXT-X-AD` o qualsiasi altro nome di tag personalizzato si trova nel flusso.
