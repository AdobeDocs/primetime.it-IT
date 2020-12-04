---
description: I flussi di file multimediali possono includere metadati aggiuntivi sotto forma di tag nella playlist o nel file manifesto, e questo file indica il posizionamento della pubblicità. Potete specificare nomi di tag personalizzati e ricevere una notifica quando determinati tag vengono visualizzati nel file manifesto.
seo-description: I flussi di file multimediali possono includere metadati aggiuntivi sotto forma di tag nella playlist o nel file manifesto, e questo file indica il posizionamento della pubblicità. Potete specificare nomi di tag personalizzati e ricevere una notifica quando determinati tag vengono visualizzati nel file manifesto.
seo-title: Tag personalizzati
title: Tag personalizzati
uuid: 103f4fff-2218-4d44-90bc-b80da467f282
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Panoramica {#custom-tags-overview}

I flussi di file multimediali possono includere metadati aggiuntivi sotto forma di tag nella playlist o nel file manifesto, e questo file indica il posizionamento della pubblicità. Potete specificare nomi di tag personalizzati e ricevere una notifica quando determinati tag vengono visualizzati nel file manifesto.

## Tag contenuto HLS {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Questa funzione non è disponibile per Safari sui computer Apple, perché TVSDK utilizza il tag video, anziché Flash o MSE, per riprodurre il contenuto HLS.

TVSDK fornisce supporto out-of-the-box per tag pubblicitari #EXT specifici. L&#39;applicazione può utilizzare tag personalizzati per migliorare il flusso di lavoro pubblicitario o per supportare scenari di blackout. Per supportare flussi di lavoro avanzati, TVSDK consente di specificare e sottoscrivere altri tag nel manifesto. Potete ricevere una notifica quando questi tag vengono visualizzati nel file manifesto.

>[!TIP]
>
>È possibile abbonarsi a tag personalizzati sia per i flussi VOD che live/lineari.

>[!NOTE]
>
>Quando HLS viene riprodotto utilizzando il tag Video in Safari e non utilizzando il Flash Fallback, questa funzione non sarà disponibile in Safari.

## Usa tag HLS personalizzati {#section_AD032318AEF5418393D2B1DF36B0BABB}

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

L’applicazione può configurare i seguenti scenari:

* Una notifica quando nel file sono presenti tag `#EXT-X-ASSET` o qualsiasi altro set di nomi di tag personalizzati a cui hai effettuato la sottoscrizione.
* Inserite annunci quando nel flusso è presente un tag `#EXT-X-AD` o qualsiasi altro nome di tag personalizzato.

Potete abbonarvi a uno dei seguenti tag come tag personalizzati: `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`. L&#39;utente riceve una notifica con un evento `TimedMetadata` durante l&#39;analisi dei file manifest.

Esistono tag pubblicitari, ad esempio `EXT-X-CUE`, ai quali si è già abbonati. Questi tag vengono utilizzati anche dal generatore di opportunità predefinito. Per specificare quali tag pubblicitari utilizzare il generatore di opportunità predefinito, è possibile impostare la proprietà `adTags`.