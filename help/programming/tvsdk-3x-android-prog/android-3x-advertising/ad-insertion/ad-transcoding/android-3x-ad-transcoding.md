---
description: Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L’inserimento di annunci Primetime e TVSDK possono tentare facoltativamente di ricompattare gli annunci incompatibili in video M3U8 compatibili.
title: Ricomprimi annunci incompatibili utilizzando Adobe Creative Repackaging Service (CRS)
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# Ricomprimi annunci incompatibili utilizzando Adobe Creative Repackaging Service (CRS) {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. L’inserimento di annunci Primetime e TVSDK possono tentare facoltativamente di ricompattare gli annunci incompatibili in video M3U8 compatibili.

Gli annunci forniti da varie terze parti, come un agenzia ad server, il tuo partner di inventario o una rete pubblicitaria, vengono spesso consegnati in formati incompatibili, come il formato MP4 per il download progressivo.

Quando TVSDK incontra per la prima volta un annuncio non compatibile, il lettore ignora l&#39;annuncio e invia una richiesta al servizio di ricompilazione creativa (CRS), che fa parte del back end di inserimento degli annunci Primetime, per ricompattare l&#39;annuncio in un formato compatibile. CRS tenta di generare più rappresentazioni del bit rate M3U8 dell’annuncio e le memorizza sulla rete CDN (Content Delivery Network) di Primetime. La prossima volta che TVSDK riceve una risposta pubblicitaria che punta a quell&#39;annuncio, il lettore utilizza la versione M3U8 compatibile con HLS dalla CDN.

Per attivare questa funzione CRS opzionale, contatta il tuo rappresentante di Adobe.

>[!NOTE]
>
>Per i clienti CRS versione 3.0 (e precedenti), a partire dalla versione 3.1 di CRS, le seguenti modifiche hanno migliorato sia la sicurezza che le prestazioni:
>
>* CRS 3.1 continua con `https:` se il contenuto in fase di reinserimento utilizza `https:`. Questo riduce il potenziale di alcuni lettori per presentare contenuti non sicuri.
   >
   >
* CRS 3.1 riduce notevolmente le chiamate di rete, migliorando il tempo di avvio del video.

>



## Abilitare CRS nelle applicazioni TVSDK {#enable-crs-in-tvsdk-applications}

Per abilitare CRS nelle applicazioni TVSDK, devi impostare le seguenti informazioni nelle impostazioni di Auditude:

1. Abilita CRS in `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
