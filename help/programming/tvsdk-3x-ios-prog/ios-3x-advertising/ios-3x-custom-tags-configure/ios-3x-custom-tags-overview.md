---
title: Esempio di risorsa VOD personalizzata
description: Esempio di risorsa VOD personalizzata
copied-description: true
exl-id: c5722e1f-75f7-40b6-861c-bbe348e1183b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '72'
ht-degree: 0%

---

# Esempio di risorsa VOD personalizzata {#example-of-a-customized-vod-asset}

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
