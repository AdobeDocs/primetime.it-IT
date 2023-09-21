---
description: Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. Primetime ad insertion e TVSDK possono opzionalmente tentare di ricompilare gli annunci incompatibili in video M3U8 compatibili.
title: Reimpacchettare annunci incompatibili utilizzando Adobe Creative Repackaging Service (CRS)
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# Reimpacchettare annunci incompatibili utilizzando Adobe Creative Repackaging Service (CRS) {#repackage-incompatible-ads-using-adobe-creative-repackaging-service-crs}

Alcuni annunci di terze parti (o creativi) non possono essere uniti nel flusso di contenuto HTTP Live Streaming (HLS) perché il loro formato video è incompatibile con HLS. Primetime ad insertion e TVSDK possono opzionalmente tentare di ricompilare gli annunci incompatibili in video M3U8 compatibili.

Gli annunci forniti da terze parti, come ad esempio un server di annunci di un&#39;agenzia, un partner di inventario o una rete di annunci, vengono spesso consegnati in formati incompatibili, come il formato MP4 per il download progressivo.

Quando TVSDK rileva per la prima volta un annuncio incompatibile, il lettore ignora l’annuncio e invia una richiesta al servizio di repackaging creativo (CRS), che fa parte del back-end di inserimento dell’annuncio Primetime, per riconfezionare l’annuncio in un formato compatibile. CRS tenta di generare più copie trasformate M3U8 a velocità bit dell’annuncio e memorizza tali copie trasformate sulla rete CDN (Content Delivery Network) Primetime. La prossima volta che TVSDK riceve una risposta dell’annuncio che punta a tale annuncio, il lettore utilizza la versione M3U8 compatibile con HLS dalla CDN.

Per attivare questa funzione CRS opzionale, contatta il rappresentante del tuo Adobe.

>[!NOTE]
>
>Per i clienti CRS versione 3.0 (e precedenti), a partire dalla versione 3.1 di CRS, le seguenti modifiche hanno migliorato sia la sicurezza che le prestazioni:
>
>* CRS 3.1 continua con `https:` se il contenuto da ricompilare utilizza `https:`. Questo riduce la possibilità che alcuni lettori presentino contenuti non sicuri.
>
>* CRS 3.1 riduce notevolmente le chiamate di rete, migliorando i tempi di avvio dei video.
>

## Abilitare CRS nelle applicazioni TVSDK {#enable-crs-in-tvsdk-applications}

Per abilitare CRS nelle applicazioni TVSDK, è necessario impostare le seguenti informazioni nelle impostazioni di Auditude:

1. Abilitare CRS in `AuditudeSettings`.

   ```
   ... 
   auditudeSettings.setCreativeRepackagingEnabled(true); 
   auditudeSettings.setCreativeRepackagingFormat("application/x-mpegURL"); 
   ```
