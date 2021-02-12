---
title: Transcodifica Just-in-Time
description: null
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# Transcodifica Just-in-Time {#just-in-time-transcoding}

Primetime  Ad Insertion offre funzionalità di transcodifica e creazione di pacchetti nel tempo per garantire la corretta riproduzione di contenuti pubblicitari incompatibili. Può anche inserire pacchetti ID3 in frammenti di annunci che possono essere utilizzati per il tracciamento annunci lato client.
Di seguito è riportato un flusso di lavoro tipico:

1.  Adobe Primetime  Ad Insertion recupera annunci pubblicitari/creativi dal server di annunci del cliente.

1. Se il formato creativo di un annuncio è nativo e compatibile con il flusso di contenuto, il creativo viene inserito nel manifesto.

1. Se il formato creativo di un annuncio non è nativo compatibile (ad esempio, .mp4, .mov, .webm), Primetime  Ad Insertion cerca una versione pre-transcodificata dell’annuncio da un CDN specificato. Se ne viene trovata una, l&#39;annuncio è inserito; in caso contrario, l’annuncio viene messo in coda per la transcodifica.

1. Dopo la transcodifica dell&#39;annuncio, Primetime  Ad Insertion unisce tutte le richieste successive per la risorsa dell&#39;annuncio ai manifesti.

Primetime  Ad Insertion supporta la transcodifica per la maggior parte dei formati video e lineari. La transcodifica creativa degli annunci avviene in genere in meno di tre minuti. Per ulteriori informazioni, contattate il rappresentante di assistenza Primetime.
