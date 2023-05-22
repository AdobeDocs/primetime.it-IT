---
description: Gli editori possono creare lettori video compatibili con HLS che funzionano con i flussi di lavoro di tracciamento degli annunci lato client del server manifest di Primetime. Le interfacce con il server manifest per i casi di streaming live e video on demand (VOD) sono leggermente diverse.
title: Panoramica del tracciamento lato client non TVSDK
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 0%

---


# Panoramica del tracciamento lato client non TVSDK {#overview-of-non-tvsdk-client-side-tracking}

Gli editori possono creare lettori video compatibili con HLS che funzionano con i flussi di lavoro di tracciamento degli annunci lato client del server manifest di Primetime. Le interfacce con il server manifest per i casi di streaming live e video on demand (VOD) sono leggermente diverse.

Il server manifesto fornisce un’API per consentire ai lettori personalizzati di richiedere i seguenti URL, che possono essere utilizzati per segnalare gli eventi di tracciamento degli annunci:

* Ad impression
* Quartile annuncio
* Avanzamento pod annuncio
* Avanzamento del pod dei contenuti

L’API del server manifest presuppone che qualsiasi lettore video che lo utilizza soddisfi i requisiti minimi. Consulta [Requisiti del lettore video](/help/primetime-ad-insertion/~old-msapi-topics/ms-player-req.md) per ulteriori dettagli.

## Flusso di lavoro di tracciamento lato client {#section_cst_flow}

![](assets/pt_ssai_notvsdk_csat_ai-workflow.png)

1. Il lettore ottiene un URL del server manifesto dal publisher.
1. Player aggiunge i parametri di query specifici ai propri requisiti di inserimento di annunci e invia una richiesta HTTP GET all’URL Bootstrap risultante. La sintassi dell&#39;URL di Bootstrap è la seguente:

   ```URL
   http{s}://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{urlSafeBase64({Content URL})}.m3u8?{query parameters}
   ```

   Ad esempio:

   ```URL
   https://manifest.auditude.com/auditude/variant/
   7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.m3u8?
   u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2&__sid__=docExample02
   ```

   L’URL include gli elementi descritti in [Invia un comando al server manifesto](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-sending-cmd.md).

1. Il server manifest stabilisce una sessione per quel lettore e genera un ID di sessione univoco. Crea una nuova variante dell’URL della playlist M3U8, che restituisce al lettore come risposta JSON. Il JSON ha la seguente sintassi:

   ```JSON
   {
    "Master-M3U8": "https://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{SessionID}/
       {urlSafeBase64(content URL)}.m3u8?u={Asset ID}&z={Zone ID}&pttrackingmode=simple&pttrackingversion=v2
       &{Any other query parameters}"
   }
   ```

   Ad esempio:

   ```JSON
   https://pcor3.manifest.auditude.com/auditude/variant/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. Il lettore utilizza l’URL della risposta JSON per richiedere la nuova variante della playlist master M3U8 dal server del manifesto.

1. Il server manifest restituisce una nuova variante M3U8 contenente gli URL della playlist a livello di flusso con una sintassi simile alla seguente:

   ```URL
   http{s}://{manifest-server:port}/auditude/{live|vod}/{PublisherAssetID}/
     {rendition}/{groupID}/{urlSafeBase64(bit rate stream URL)}.m3u8?u={Ad Request Id}&z={Ad Zone Id}&{Any other query parameters}
   ```

   Ad esempio:

   ```URL
   #EXTM3U
   #EXT-X-VERSION:5
   #EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,DEFAULT=YES,FORCED=NO,LANGUAGE="eng",URI="https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/webvtt/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvd2VidnR0L1RPUy1lbjIubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2"
   #EXT-X-STREAM-INF:BANDWIDTH=10000000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/10000/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMTAwMDAvdG9jXzEwMDAwLm0zdTg.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=1300000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/1300/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMTMwMC90b2NfMTMwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=3400000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/3400/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMzQwMC90b2NfMzQwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=2100000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/2100/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMjEwMC90b2NfMjEwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=800000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/800/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvODAwL3RvY184MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=5000000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/5000/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwMC90b2NfNTAwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=7500000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/7500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNzUwMC90b2NfNzUwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=500000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. Il lettore seleziona l’URL del manifesto a livello di flusso con velocità in bit singola appropriato per la riproduzione di contenuti ad-stitched. Ad esempio:

   ```URL
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. Il server manifesto restituisce un manifesto a livello di flusso contenente collegamenti al contenuto e collegamenti ai segmenti di Servizi terminal. Ad esempio:

   ```
      #EXTM3U
   #EXT-X-VERSION:3
   #EXT-X-TARGETDURATION:8
   #EXT-X-PLAYLIST-TYPE:VOD
   
   #EXT-X-DISCONTINUITY
   #EXTINF:8,
   https://primetime-a.akamaihd.net/assets/repackage/production/zen/195/10516675/2ac89785ee8df17a31b2594c61f6921e-300k-00001.ts
   #EXTINF:7,
   https://primetime-a.akamaihd.net/assets/repackage/production/zen/195/10516675/2ac89785ee8df17a31b2594c61f6921e-300k-00002.ts
   
   #EXT-X-DISCONTINUITY
   #EXTINF:4,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.0.ts
   #EXTINF:4,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.4000.ts
   #EXTINF:4.833,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.8000.ts   
   ```

   >[!NOTE]
   >
   >Il lettore seleziona l’URL della playlist a livello di flusso per ottenere il flusso di contenuto. Il server manifest recupera la playlist originale dalla rete CDN. Alcuni codificatori possono inserire ulteriori dettagli nel `#EXTINF` attributo titolo, ad esempio:
   >
   >
   ```
   >#EXTINF:6.006,LTC=2017-08-23T13:25:47+00:00
   >```

   Poiché il server manifesto non può dedurre il significato degli attributi non standard per modificarli nella playlist con unione di annunci, il server manifesto rimuove tutti gli attributi aggiuntivi oltre alle informazioni sulla durata in questo tag. Consulta la [EXTINF](https://tools.ietf.org/html/rfc8216#section-4.3.2.1) per ulteriori dettagli, inserire la voce nella specifica HLS.

1. Per richiedere informazioni di tracciamento, il lettore aggiunge il parametro di query `pttrackingposition` con qualsiasi valore alfanumerico nell’URL della playlist a livello di flusso per il bitrate selezionato. Ad esempio:

   ```URL
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d
   &z=173475&pttrackingmode=simple&pttrackingversion=v2&pttrackingposition=1
   ```

1. Il server manifesto restituisce il file della playlist compilato con un  [JSON](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md) o [VMAP](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md) oggetto contenente i dati di tracciamento degli annunci per il file m3u8 a livello di flusso attualmente richiesto.

   >[!NOTE]
   >
   >Il server manifesto genera oggetti di tracciamento degli annunci solo se gli annunci sono stati inseriti nella playlist a livello di flusso attualmente richiesta. Se il lettore riproduce una playlist che non contiene annunci inseriti, il server manifest restituisce lo stato HTTP 201 per la richiesta della playlist di tracciamento degli annunci. Se il lettore effettua la richiesta di tracciamento dell’annuncio per un flusso che non sta riproducendo, il server manifest restituirà lo stato HTTP 500. Ad esempio, se la richiesta di riproduzione corrente è per 500.m3u8, il server manifesto restituisce un JSON|VMAP nella 500.m3u8 per la richiesta di tracciamento degli annunci. Tuttavia, se il lettore passa successivamente ai flussi per riprodurre 800.m3u8, le informazioni di tracciamento dell’annuncio nel 500.m3u8 non sono più valide, generando un errore 404.

   >[!NOTE]
   >
   >Il server manifesto genera l&#39;oggetto di tracciamento dell&#39;annuncio in base al `pttrackingversion` valore nell’URL di Bootstrap. Se il `pttrackingversion` viene omesso o ha un valore non valido, il server manifesto compilerà automaticamente le informazioni di tracciamento degli annunci in `#EXT-X-MARKER` in ogni playlist a livello di flusso richiesta. Consulta [per ulteriori dettagli](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/ms-api-playlists.md).

1. Il lettore richiede ogni URL di tracciamento dell’annuncio per ogni evento di tracciamento dell’annuncio al momento giusto.

>[!NOTE]
>
>Per i flussi in diretta, il lettore deve ripetere i passaggi da 6 a 10 in quanto il responsabile del pacchetto aggiorna costantemente la playlist per tutta la durata dell’evento in diretta.

Durante la riproduzione del video, il lettore deve tenere traccia della posizione della testina di riproduzione e utilizzarla insieme agli URL di tracciamento ricevuti dall’inserimento di annunci di Primetime. Gli URL di tracciamento sono raggruppati per scostamento temporale dall’inizio della riproduzione. Per ogni offset temporale, esiste un URL per ogni sistema di annunci a cui inviare le informazioni di tracciamento. Ulteriori dettagli sul formato differiscono tra video live e video on-demand.
