---
title: Guida introduttiva  Adobe Primetime  Ad Insertion
description: Guida introduttiva a  Adobe Primetime  Ad Insertion
translation-type: tm+mt
source-git-commit: 2a9bb089cda2b315f91b30d5cab0db9b3e372799
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---


# Guida introduttiva  Adobe Primetime  Ad Insertion {#ptai-get-started}

Primetime  Ad Insertion coordina i sistemi che forniscono contenuti e annunci per creare esperienze pubblicitarie personalizzate e in streaming, quindi monitora la riproduzione degli annunci per i tuoi inserzionisti.

Primetime  Ad Insertion interagisce con le applicazioni client per la distribuzione di video riscrivendo i manifesti video per fornire annunci mirati ed esperienze personalizzate per ciascun visualizzatore. Questi manifesti combinano contenuti e annunci inviati da un server di annunci e possono includere facoltativamente metadati contenenti istruzioni dettagliate per il tracciamento di annunci. Primetime  Ad Insertion supporta sia il monitoraggio degli annunci lato client che lato server.

Una volta configurato correttamente il sistema, il flusso di lavoro tipico potrebbe essere il seguente:

1. L&#39;applicazione client genera un URL [di](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md) Bootstrap con informazioni sul flusso video e invia una richiesta di GET a Primetime  Ad Insertion.

1. Primetime  Ad Insertion risponde inviando il manifesto di contenuto dalla CDN dell&#39;editore all&#39;applicazione client.

1. L&#39;applicazione client sceglie i flussi appropriati nel manifesto generato per la riproduzione ed effettua richieste al Ad Insertion Primetime .

1. Primetime  Ad Insertion recupera i flussi richiesti dalla CDN del contenuto, analizza/legge eventuali informazioni sui cue point, effettua chiamate al server degli annunci e sostituisce le interruzioni di annunci se necessario.

1. Primetime  Ad Insertion normalizza il manifesto riscrivendo gli URL delle risorse e rilevando se le creatività degli annunci richiedono la transcodifica. <!-- see [Just-in-time ad transcoding](just-in-time-transcoding.md) and [packaging](just-in-time-repackaging.md).-->

1. Primetime  Ad Insertion recupera gli annunci pubblicitari richiesti e inserisce i frammenti appropriati nei manifesti.

1. Primetime  Ad Insertion consegna i manifesti cuciti finali, inclusi gli annunci pubblicitari, all&#39;applicazione client per la riproduzione.

1. La distribuzione e la visibilità degli annunci possono essere misurate tramite il monitoraggio degli annunci lato client o lato server, consultate [Impostazione del tracciamento](set-up-ad-tracking.md)degli annunci.

Primetime  Ad Insertion supporta la maggior parte delle configurazioni client per HLS/DASH.
