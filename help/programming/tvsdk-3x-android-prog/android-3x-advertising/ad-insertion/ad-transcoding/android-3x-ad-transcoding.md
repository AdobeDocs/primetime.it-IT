---
description: Alcuni annunci (o creativi) di terze parti non possono essere inseriti nello streaming di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L'inserimento di annunci Primetime e TVSDK possono eventualmente tentare di ricompilare annunci incompatibili in video M3U8 compatibili.
seo-description: Alcuni annunci (o creativi) di terze parti non possono essere inseriti nello streaming di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L'inserimento di annunci Primetime e TVSDK possono eventualmente tentare di ricompilare annunci incompatibili in video M3U8 compatibili.
seo-title: Reimballaggio di annunci incompatibili con  Adobe Creative Repackaging Service (CRS)
title: Reimballaggio di annunci incompatibili con  Adobe Creative Repackaging Service (CRS)
uuid: ef542d13-6d52-4429-8a1e-0af2df236f12
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Reimballaggio di annunci incompatibili con  Adobe Creative Repackaging Service (CRS) {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

Alcuni annunci (o creativi) di terze parti non possono essere inseriti nello streaming di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L&#39;inserimento di annunci Primetime e TVSDK possono eventualmente tentare di ricompilare annunci incompatibili in video M3U8 compatibili.

Gli annunci inviati da varie terze parti, come un&#39;agenzia pubblicitaria server, il partner di magazzino o una rete di annunci, vengono spesso consegnati in formati incompatibili, come il formato MP4 per lo scaricamento progressivo.

Quando TVSDK incontra per la prima volta un annuncio incompatibile, il lettore ignora l&#39;annuncio e invia una richiesta al servizio di reimballaggio creativo (CRS), che fa parte del back end di inserimento annunci Primetime, per reassemblare l&#39;annuncio in un formato compatibile. CRS tenta di generare più rappresentazioni M3U8 con bitrate dell’annuncio e memorizza tali rappresentazioni nella rete CDN (Primetime Content Delivery Network). Alla successiva ricezione di una risposta di annuncio da parte di TVSDK, il lettore utilizza la versione M3U8 compatibile con HLS dalla CDN.

Per attivare questa funzione opzionale CRS, contattate il rappresentante del Adobe .

>[!NOTE]
>
>Per i clienti CRS versione 3.0 (e versioni precedenti), a partire dalla versione 3.1 di CRS, le seguenti modifiche hanno migliorato la sicurezza e le prestazioni:
>
>* CRS 3.1 continua con `https:` se il contenuto in fase di reinserimento utilizza `https:`. Questo riduce il potenziale di alcuni lettori per presentare contenuto non sicuro.
   >
   >
* CRS 3.1 riduce notevolmente le chiamate di rete, migliorando i tempi di avvio del video.

>



Per ulteriori informazioni sui CRS, vedere [Creative Packaging Service (CRS)](../../../../../dynamic-ad-insertion/creative-repackaging-service/crs-overview.md).

## Attivare CRS nelle applicazioni TVSDK {#enable-crs-in-tvsdk-applications}

Per abilitare CRS nelle applicazioni TVSDK, nelle impostazioni di Auditude devi impostare le seguenti informazioni:

1. Attivare CRS in `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
