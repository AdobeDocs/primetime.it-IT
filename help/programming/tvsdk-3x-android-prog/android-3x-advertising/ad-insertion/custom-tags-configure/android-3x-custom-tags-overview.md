---
seo-title: Esempio di una risorsa VOD personalizzata
title: Esempio di una risorsa VOD personalizzata
uuid: 25927d5f-ac16-45f4-bf0d-92f1ab394c05
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---


# Esempio di una risorsa VOD personalizzata{#example-of-a-customized-vod-asset}

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

* Una notifica quando nel file sono presenti tag `#EXT-X-ASSET` o qualsiasi altro set di nomi di tag personalizzati a cui hai effettuato la sottoscrizione.
* Inserite annunci quando nel flusso è presente un tag `#EXT-X-AD` o qualsiasi altro nome di tag personalizzato.

