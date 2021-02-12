---
title: Guida introduttiva  Adobe Primetime  Ad Insertion
description: Guida introduttiva a  Adobe Primetime  Ad Insertion
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---


# Guida introduttiva  Ad Insertion Adobe Primetime  {#ptai-get-started}

Primetime  Ad Insertion coordina i sistemi che forniscono contenuti e annunci per creare esperienze pubblicitarie personalizzate e in streaming, quindi monitora la riproduzione degli annunci per i tuoi inserzionisti.

Primetime  Ad Insertion interagisce con le applicazioni client per la distribuzione di video riscrivendo i manifesti video per fornire annunci mirati ed esperienze personalizzate per ciascun visualizzatore. Questi manifesti combinano contenuti e annunci inviati da un server di annunci e possono includere facoltativamente metadati contenenti istruzioni dettagliate per il tracciamento di annunci. Primetime  Ad Insertion supporta sia il monitoraggio degli annunci lato client che lato server.

Una volta configurato correttamente il sistema, il flusso di lavoro tipico potrebbe essere il seguente:

1. L&#39;applicazione client genera un [URL di Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) con informazioni sul flusso video e invia una richiesta di GET a Primetime  Ad Insertion.  Primetime  Ad Insertion supporta HLS e DASH con diversi formati di segnalamento pubblicitario.

1. Primetime  Ad Insertion risponde inviando il manifesto di contenuto dalla CDN dell&#39;editore all&#39;applicazione client.

1. L&#39;applicazione client sceglie i flussi appropriati nel manifesto generato per la riproduzione ed effettua richieste al Ad Insertion Primetime .

1. Primetime  Ad Insertion recupera i flussi richiesti dalla CDN del contenuto, analizza/legge eventuali informazioni sui cue point, effettua chiamate al server degli annunci e sostituisce le interruzioni di annunci se necessario.

1. Primetime  Ad Insertion normalizza il manifesto riscrivendo gli URL delle risorse e rilevando se la transcodifica è necessaria per gli annunci pubblicitari, vedi [Transcodifica ad hoc](/help/primetime-ad-insertion/just-in-time-transcoding/jit-transcoding-overview.md).

1. Primetime  Ad Insertion recupera gli annunci pubblicitari richiesti e inserisce i frammenti appropriati nei manifesti.

1. Primetime  Ad Insertion consegna i manifesti cuciti finali, inclusi gli annunci pubblicitari, all&#39;applicazione client per la riproduzione.

1. La distribuzione e la visualizzabilità degli annunci possono essere misurate tramite il monitoraggio degli annunci lato client o lato server. Consultate [Setting up Ad Tracking](/help/primetime-ad-insertion/getting-started/set-up-ad-tracking.md) (Impostazione del tracciamento degli annunci).

Primetime  Ad Insertion supporta la maggior parte delle configurazioni di client e lettore HLS/DASH. Per ulteriori informazioni sui formati di segnalazione di annunci supportati, vedi [Formati di cue supportati](/help/primetime-ad-insertion/getting-started/ad-insertion-live-linear-stream.md).
