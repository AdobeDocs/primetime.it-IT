---
title: Introduzione ad Adobe Primetime Ad Insertion
description: Guida introduttiva di Adobe Primetime Ad Insertion
exl-id: 629ea2a5-1b50-4451-a478-95d02f192145
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Introduzione ad Adobe Primetime Ad Insertion {#ptai-get-started}

Primetime Ad Insertion coordina i sistemi che forniscono contenuti e annunci per creare esperienze pubblicitarie personalizzate in-stream e quindi tracciare la riproduzione degli annunci per gli inserzionisti.

Primetime Ad Insertion interagisce con le applicazioni client di consegna video riscrivendo i manifesti video per fornire annunci mirati ed esperienze personalizzate per ogni visualizzatore. Questi manifesti combinano contenuti e annunci distribuiti da un ad server e possono facoltativamente includere metadati contenenti istruzioni dettagliate per il tracciamento degli annunci. Primetime Ad Insertion supporta il tracciamento degli annunci lato client e lato server.

Una volta configurato correttamente il sistema, un flusso di lavoro tipico potrebbe presentarsi come segue:

1. L’applicazione client genera un [BOOTSTRAP URL](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) con informazioni sul flusso video e invia una richiesta GET all’Ad Insertion Primetime.  Primetime Ad Insertion supporta HLS e DASH con diversi formati di segnalazione pubblicitaria.

1. L’Ad Insertion di Primetime risponde inviando nuovamente il manifesto del contenuto dalla rete CDN dell’editore all’applicazione client.

1. L’applicazione client sceglie i flussi appropriati da riprodurre nel manifesto generato e invia le richieste all’Ad Insertion Primetime.

1. Primetime Ad Insertion recupera i flussi richiesti dalla rete CDN del contenuto, analizza/legge eventuali informazioni sui cue, effettua chiamate al server dell’annuncio e sostituisce gli annunci interrotti in base alle necessità.

1. Primetime Ad Insertion normalizza il manifesto riscrivendo gli URL delle risorse e rilevando se le creatività degli annunci richiedono la transcodifica, vedi [Transcodifica annunci just-in-time](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md).

1. Primetime Ad Insertion recupera le creatività dell’annuncio richieste e inserisce i frammenti appropriati nei manifesti.

1. Primetime Ad Insertion distribuisce i manifesti uniti finali, inclusi gli annunci, all’applicazione client per la riproduzione.

1. La distribuzione e la visualizzabilità degli annunci possono essere misurate tramite il tracciamento degli annunci lato client o lato server, vedi [Impostazione del tracciamento degli annunci](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md).

Primetime Ad Insertion supporta la maggior parte delle configurazioni del client e del lettore HLS/DASH. Per ulteriori informazioni sui formati di segnalazione pubblicitaria specifici supportati, consulta [Formati cue supportati](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md).
