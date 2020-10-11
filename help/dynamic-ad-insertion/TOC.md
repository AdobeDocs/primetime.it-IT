---
cloud: experience-cloud
product: adobe primetime
audience: end-user
user-guide-title: Primetime Dynamic  Ad Insertion Help
user-guide-description: Explains how to monetize content by inserting user-targeted dynamic ads on the server and engage audience with personalized ads.
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Guida per Ad Insertion  dinamici {#ad-insertion}

+ [Panoramica Ad Insertion  dinamico](home.md)
+ Introduzione a Primetime  Ad Insertion{#get-started}
   + [Panoramica](get-started-ptai.md)
   + [Preparare l&#39;utilizzo di Primetime  Ad Insertion](setup-ptai.md)
   + [Integrare il server di annunci](integrate-ad-server.md)
   + [Integrare la rete CDN](integrate-cdn.md)
   + [Utilizzare l&#39;inserimento di annunci nei flussi live/lineari](ad-insertion-live-linear-stream.md)
   + [Usa inserimento annunci per VOD](ad-insertion-vod.md)
   + [Configurare il tracciamento degli annunci](set-up-ad-tracking.md)
+ [Note sulla versione di Ad Insertion  dinamici](https://docs.adobe.com/content/help/en/primetime/release-notes/ptai/ptai-19x-release-notes.html)
+ [Strumento di debug server manifesto](manifest-server-debugging-tool.md)

<!-- + [Server Side Ad Insertion debugging dashboard](ssai-debugging-dashboard.md)-->
+ Manifest Server API for  Ad Insertion {#manifest-server}
   + [Panoramica delle interazioni del server manifesto](msapi-topics/ms-overview.md)
   + Guida introduttiva al server manifesto {#get-started}
      + [Invio di un comando al server manifesto](msapi-topics/ms-getting-started/ms-sending-cmd.md)
      + [Parametri query server manifesto](msapi-topics/ms-getting-started/ms-api-query-params.md)
   + Richieste di inserimento annunci {#ad-insert}
      + [Richieste di inserimento annunci](msapi-topics/ms-insert-ads/ms-ad-insert.md)
      + [Parametri di query opzionali per client e situazione](msapi-topics/ms-insert-ads/ms-api-query-param-situation.md)
      + [Facilitazione del passaggio del lettore HLS ai flussi di failover/backup](msapi-topics/ms-insert-ads/hls-switching-to-failover.md)
      + [Flussi bitrate multipli](msapi-topics/ms-insert-ads/ms-api-mbr-streams.md)
      + [Inserimento interruzione annuncio parziale](msapi-topics/ms-insert-ads/partial-ad-break-insetion.md)
      + [Supporto CDN multiplo per la distribuzione di annunci CRS](msapi-topics/ms-insert-ads/ms-api-multi-cdns-for-crs.md)
   + Sostituisci timeline VOD {#replace-vod}
      + [Modifiche al VOD](msapi-topics/ms-changes-vod-timeline/ms-replace-vod-timeline.md)
      + [Formato della timeline VOD](msapi-topics/ms-changes-vod-timeline/ms-api-timeline-format.md)
      + [Sostituire una timeline VOD](msapi-topics/ms-changes-vod-timeline/t-ms-replace-vod-timeline.md)
   + Tracciamento efficacia annuncio {#ad}
      + [Tracciamento annunci](msapi-topics/ms-at-effectiveness/ms-at-overview.md)
      + [Abilita tracciamento annunci lato client](msapi-topics/ms-at-effectiveness/ms-enable-client-side-ad-tracking.md)
      + [Panoramica del tracciamento lato client non TVSDK](msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md)
      + [API per l&#39;interazione dei lettori con il server manifesto](msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md)
      + [Direttiva EXT-X MARKER](msapi-topics/ms-at-effectiveness/ms-api-playlists.md)
   + [Cookie](msapi-topics/ms-cookies.md)
   + [Supporto per le didascalie WebVTT](msapi-topics/ms-webvtt-captions.md)
   + Elenco dei formati di file {#list}
      + [Formati di file](msapi-topics/ms-list-file-formats/ms-api-file-formats.md)
      + [Formato JSON per l&#39;URL per la richiesta di playlist con manifesto variante](msapi-topics/ms-list-file-formats/ms-json-m3u8.md)
      + [Formati JSON per il tracciamento degli URL](msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md)
      + [Formato VMAP per il tracciamento degli URL](msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md)
   + [Requisiti del lettore video](msapi-topics/ms-player-req.md)
+ Primetime Creative Repackaging Service {#crs}
   + [Panoramica del CRS](creative-repackaging-service/crs-overview.md)
   + [Principali utilizzi del CRS](creative-repackaging-service/jit-async-hls-conv.md)
   + [Supporto per più CDN](creative-repackaging-service/multi-cdn-supportt.md)
   + [Flussi di lavoro dettagliati per il reimballaggio JIT](creative-repackaging-service/jit-repackage.md)
   + [Utilizzo di CRS per inserire tag di metadati temporizzati ID3](creative-repackaging-service/inject-id3.md)
   + [API di ricompilazione](creative-repackaging-service/api-repackage.md)
