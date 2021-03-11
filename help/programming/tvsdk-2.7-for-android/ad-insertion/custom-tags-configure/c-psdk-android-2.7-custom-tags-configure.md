---
description: I flussi di file multimediali possono includere metadati aggiuntivi sotto forma di tag nella playlist o nel file manifest, e questo file indica il posizionamento della pubblicità. Puoi specificare nomi di tag personalizzati da avvisare quando alcuni tag compaiono nel file manifesto.
title: Tag personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# Panoramica {#custom-tags-overview}

I flussi di file multimediali possono includere metadati aggiuntivi sotto forma di tag nella playlist o nel file manifest, e questo file indica il posizionamento della pubblicità. Puoi specificare nomi di tag personalizzati da avvisare quando alcuni tag compaiono nel file manifesto.

## Tag del contenuto HLS {#section_E99299152089418FBA56F5F09FC547B0}

>[!IMPORTANT]
>
>Questa funzione non è disponibile per Safari nei computer Apple, perché per riprodurre il contenuto HLS TVSDK utilizza il tag video, anziché il Flash o MSE.

TVSDK fornisce supporto predefinito per tag pubblicitari specifici `#EXT`. L&#39;applicazione può utilizzare tag personalizzati per migliorare il flusso di lavoro pubblicitario o per supportare scenari di blackout. Per supportare flussi di lavoro avanzati, TVSDK consente di specificare e sottoscrivere tag aggiuntivi nel manifesto. Puoi ricevere notifiche quando questi tag compaiono nel file manifesto.

>[!TIP]
>
>Puoi abbonarti a tag personalizzati sia per i flussi VOD che per quelli live/lineari.

>[!NOTE]
>
>Quando HLS viene riprodotto utilizzando il tag Video in Safari e non utilizzando Flash Fallback, questa funzione non sarà disponibile in Safari.

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

* Nel file è presente una notifica quando sono presenti tag `#EXT-X-ASSET` o qualsiasi altro set di nomi di tag personalizzati a cui hai effettuato la sottoscrizione.
* Inserisci annunci quando nel flusso è presente un tag `#EXT-X-AD` o qualsiasi altro nome di tag personalizzato.

Puoi abbonarti a uno dei seguenti tag come tag personalizzati:

* `EXT-PROGRAM-DATE-TIME`
* `EXT-X-START`
* `EXT-X-AD`
* `EXT-X-CUE`
* `EXT-X-ENDLIST`

Verrà notificato un evento `TimedMetadata` durante l&#39;analisi dei file manifest.

Esistono alcuni tag pubblicitari, ad esempio `EXT-X-CUE`, ai quali sei già iscritto. Questi tag ad vengono utilizzati anche dal generatore di opportunità predefinito. Puoi specificare quali tag di annunci vengono utilizzati dal generatore di opportunità predefinito impostando la proprietà `adTags` .
