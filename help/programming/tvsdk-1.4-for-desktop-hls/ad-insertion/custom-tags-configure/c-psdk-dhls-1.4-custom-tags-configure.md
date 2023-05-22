---
description: I flussi multimediali possono contenere metadati aggiuntivi sotto forma di tag nel file di playlist/manifesto e questo file indica il posizionamento della pubblicità. È possibile specificare nomi di tag personalizzati e ricevere una notifica quando determinati tag vengono visualizzati nel file manifesto.
title: Tag personalizzati
exl-id: 1b660b2a-c48b-49f9-af14-8b2318119e9a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# Tag personalizzati{#custom-tags}

I flussi multimediali possono contenere metadati aggiuntivi sotto forma di tag nel file di playlist/manifesto e questo file indica il posizionamento della pubblicità. È possibile specificare nomi di tag personalizzati e ricevere una notifica quando determinati tag vengono visualizzati nel file manifesto.

## Tag di contenuto HLS {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Questa funzione non è disponibile per Safari su computer Apple, perché TVSDK utilizza il tag video, anziché Flash o MSE, per riprodurre contenuti HLS.

TVSDK fornisce supporto predefinito per tag pubblicitari di #EXT specifici. L’applicazione può utilizzare tag personalizzati per migliorare il flusso di lavoro della pubblicità o per supportare scenari di sospensione attività. Per supportare flussi di lavoro avanzati, TVSDK consente di specificare e sottoscrivere tag aggiuntivi nel manifesto. Puoi ricevere una notifica quando questi tag vengono visualizzati nel file manifesto.

>[!TIP]
>
>Puoi abbonarti a tag personalizzati sia per VOD che per flussi live/lineari.

>[!NOTE]
>
>Quando HLS viene riprodotto utilizzando il tag Video in Safari e non il Flash Fallback, questa funzione non sarà disponibile in Safari.

## Utilizzo di tag HLS personalizzati {#section_AD032318AEF5418393D2B1DF36B0BABB}

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

L&#39;applicazione può impostare i seguenti scenari:

* Una notifica quando `#EXT-X-ASSET` I tag, o qualsiasi altro insieme di nomi di tag personalizzati a cui ti sei iscritto, sono già presenti nel file.
* Inserisci annunci quando un `#EXT-X-AD` o qualsiasi altro nome di tag personalizzato si trova nel flusso.

È possibile sottoscrivere uno qualsiasi dei seguenti tag come tag personalizzati: `EXT-PROGRAM-DATE-TIME`, `EXT-X-START`, `EXT-X-AD`, `EXT-X-CUE`, `EXT-X-ENDLIST`. Viene inviata una notifica con `TimedMetadata` durante l&#39;analisi dei file manifest.

Ci sono alcuni tag pubblicitari, come `EXT-X-CUE`, a cui si è già iscritti. Questi tag di annuncio vengono utilizzati anche dal generatore di opportunità predefinito. È possibile specificare quali tag di annunci vengono utilizzati dal generatore di opportunità predefinito impostando `adTags` proprietà.
