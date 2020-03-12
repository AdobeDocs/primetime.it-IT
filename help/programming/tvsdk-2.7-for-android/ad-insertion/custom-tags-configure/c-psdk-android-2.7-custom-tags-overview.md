---
seo-title: Esempio di una risorsa VOD personalizzata
title: Esempio di una risorsa VOD personalizzata
uuid: 21e83b47-d7e2-4a2d-8a0b-80dd09e253a8
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Esempio di una risorsa VOD personalizzata {#example-of-a-customized-vod-asset}

Esempio di una risorsa VOD personalizzata:

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

* Una notifica relativa all&#39;esistenza nel file di `#EXT-X-ASSET` tag o altri set di nomi di tag personalizzati sottoscritti.
* Inserite annunci quando un `#EXT-X-AD` tag, o qualsiasi altro nome di tag personalizzato, viene trovato nel flusso.

