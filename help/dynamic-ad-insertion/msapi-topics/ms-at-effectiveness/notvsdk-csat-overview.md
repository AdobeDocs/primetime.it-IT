---
description: Gli editori possono creare lettori video compatibili con HLS che utilizzano i flussi di lavoro di tracciamento annunci lato client del server manifesto Primetime. Le interfacce con il server manifesto per i casi di streaming live e video on demand (VOD) sono leggermente diverse.
seo-description: Gli editori possono creare lettori video compatibili con HLS che utilizzano i flussi di lavoro di tracciamento annunci lato client del server manifesto Primetime. Le interfacce con il server manifesto per i casi di streaming live e video on demand (VOD) sono leggermente diverse.
seo-title: Panoramica del tracciamento lato client non TVSDK
title: Panoramica del tracciamento lato client non TVSDK
uuid: fb23be01-3327-443d-82c4-fb0993e7fec1
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# Panoramica del tracciamento lato client non TVSDK {#overview-of-non-tvsdk-client-side-tracking}

Gli editori possono creare lettori video compatibili con HLS che utilizzano i flussi di lavoro di tracciamento annunci lato client del server manifesto Primetime. Le interfacce con il server manifesto per i casi di streaming live e video on demand (VOD) sono leggermente diverse.

Il server manifest fornisce un&#39;API per consentire ai lettori personalizzati di richiedere i seguenti URL, che possono utilizzare per segnalare gli eventi di tracciamento annunci:

* Ad impression
* Annuncio quartile
* Stato del contenitore annuncio
* Avanzamento del contenitore Contenuto

L&#39;API del server manifesto presuppone che qualsiasi lettore video che lo utilizza soddisfi i requisiti minimi. Per ulteriori informazioni, vedere [Requisiti del lettore video](../../msapi-topics/ms-player-req.md).

## Flusso di lavoro di tracciamento lato client {#section_cst_flow}

![](assets/pt_ssai_notvsdk_csat_ai-workflow.png)

1. Player ottiene un URL del server manifesto dall’editore.
1. Player aggiunge parametri di query specifici ai relativi requisiti di inserimento annunci e invia una richiesta di GET HTTP all&#39;URL di Bootstrap risultante. L&#39;URL Bootstrap ha la sintassi seguente:

   ```
   http{s}://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{urlSafeBase64({Content URL})}.m3u8?{query parameters}
   
   For example:
   https://manifest.auditude.com/auditude/variant/
   7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.m3u8?
   u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2&__sid__=docExample02
   ```

   L&#39;URL include gli elementi descritti in [Invia un comando al server manifesto](../../msapi-topics/ms-getting-started/ms-sending-cmd.md).

1. Il server manifesto stabilisce una sessione per quel lettore e genera un ID sessione univoco. Crea una nuova variante dell&#39;URL della playlist M3U8, che ritorna al lettore come risposta JSON. Il JSON ha la sintassi seguente:

   ```
   {
    "Master-M3U8": "https://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{SessionID}/
       {urlSafeBase64(content URL)}.m3u8?u={Asset ID}&z={Zone ID}&pttrackingmode=simple&pttrackingversion=v2
       &{Any other query parameters}"
   }
   
   For example:
   https://pcor3.manifest.auditude.com/auditude/variant/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. Player utilizza l&#39;URL della risposta JSON per richiedere la nuova playlist master variante M3U8 dal server manifesto.
1. Il server di manifesto restituisce una nuova variante M3U8 contenente URL playlist a livello di flusso con una sintassi simile a quella seguente:

   ```
   http{s}://{manifest-server:port}/auditude/{live|vod}/{PublisherAssetID}/
     {rendition}/{groupID}/{urlSafeBase64(bit rate stream URL)}.m3u8?u={Ad Request Id}&z={Ad Zone Id}&{Any other query parameters}
   
   For example:
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

1. Il lettore seleziona l&#39;URL manifesto a livello di flusso e con bitrate singolo appropriato per la riproduzione del contenuto ad-cucite. Ad esempio:

   ```
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. Il server del manifesto restituisce un manifesto a livello di flusso contenente collegamenti al contenuto e ai collegamenti ai segmenti TS degli annunci. Ad esempio:

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
   >Il lettore seleziona l&#39;URL della playlist a livello di flusso per ottenere il flusso di contenuto. Il server manifesto recupera la playlist originale dalla rete CDN. Alcuni codificatori possono inserire ulteriori dettagli nell&#39;attributo del titolo `#EXTINF`, ad esempio:
   >
   >
   ```
   >#EXTINF:6.006,LTC=2017-08-23T13:25:47+00:00
   >```

   Poiché il server di manifesto non è in grado di identificare il significato degli attributi non standard per modificarli per la playlist con punti di interesse, il server di manifesto rimuove tutti gli attributi aggiuntivi oltre le informazioni sulla durata in questo tag. Per ulteriori informazioni, vedere la voce [EXTINF](https://tools.ietf.org/html/rfc8216#section-4.3.2.1) nella specifica HLS.


1. Per richiedere informazioni di tracciamento, il lettore aggiunge il parametro di query `pttrackingposition` con qualsiasi valore alfanumerico all&#39;URL della playlist a livello di flusso per il bitrate selezionato. Ad esempio:

   ```
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d
   &z=173475&pttrackingmode=simple&pttrackingversion=v2&pttrackingposition=1
   ```

1. Il server del manifesto restituisce il file playlist compilato con un oggetto [JSON](../../msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md) o [VMAP](../../msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md) contenente i dati di tracciamento annunci per il file m3u8 a livello di flusso attualmente richiesto.

   >[!NOTE]
   >
   >Il server manifesto genererà oggetti di tracciamento annunci solo se gli annunci sono stati inseriti nella playlist a livello di flusso richiesta. Se il lettore riproduce una playlist che non contiene annunci inseriti, il server manifesto restituisce uno stato HTTP 201 per la richiesta della playlist di tracciamento annunci. Se il lettore effettua la richiesta di tracciamento annunci per un flusso che non viene riprodotto, il server manifesto restituisce uno stato HTTP 500. Ad esempio, se la richiesta di riproduzione corrente è per 500.m3u8, il server manifesto restituisce un JSON|VMAP in 500.m3u8 per la richiesta di tracciamento annunci. Tuttavia, se il lettore passa successivamente al flusso per riprodurre il file 800.m3u8, le informazioni di tracciamento degli annunci nel file 500.m3u8 diventano non valide, generando un errore 404.

   >[!NOTE]
   >
   >Il server manifesto genera l&#39;oggetto di tracciamento degli annunci in base al valore `pttrackingversion` nell&#39;URL di Bootstrap. Se `pttrackingversion` viene omesso o ha un valore non valido, il server manifesto compila automaticamente le informazioni di tracciamento annunci nei tag `#EXT-X-MARKER` in ogni playlist a livello di flusso richiesta. Vedere [per ulteriori dettagli](../../msapi-topics/ms-at-effectiveness/ms-api-playlists.md).

1. Il lettore richiede ogni URL di tracciamento annunci per ogni evento di tracciamento annunci al momento opportuno.

>[!NOTE]
>
>Per i flussi dal vivo, il lettore deve ripetere i passaggi da 6 a 10 in quanto il packager aggiorna costantemente la playlist per tutta la durata dell&#39;evento dal vivo.

Durante la riproduzione del video, il lettore deve tenere traccia della posizione dell&#39;indicatore di riproduzione e utilizzare questa posizione insieme agli URL di tracciamento ricevuti da Primetime e dall&#39;inserimento di annunci. Gli URL di tracciamento sono raggruppati per scostamento temporale dall’inizio della riproduzione. Per ogni offset temporale, è presente un URL per ogni sistema di annunci a cui inviare le informazioni di tracciamento. Ulteriori dettagli sul formato sono diversi tra video live e video on demand.
