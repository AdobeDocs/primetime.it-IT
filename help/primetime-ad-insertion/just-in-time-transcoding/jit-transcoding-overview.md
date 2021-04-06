---
title: Transcodifica just-in-time
description: Transcodifica just-in-time
copied-description: true
exl-id: 9577e1d5-1462-49d6-9d24-94e74dc9c019
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Transcodifica just-in-time {#just-in-time-transcoding}

Primetime Ad Insertion offre funzioni di transcodifica e packaging just-in-time per garantire la corretta riproduzione degli annunci pubblicitari incompatibili nei flussi di contenuto. Può anche inserire pacchetti ID3 nei frammenti di annunci che possono essere utilizzati nel monitoraggio degli annunci lato client.
Un flusso di lavoro tipico è il seguente:

1. Adobe Primetime Ad Insertion recupera gli annunci/creativi dal server di annunci del cliente.

1. Se il formato creativo di un annuncio è nativamente compatibile con il flusso di contenuto, il creativo viene inserito nel manifesto.

1. Se il formato creativo di un annuncio non è nativamente compatibile (ad esempio, .mp4, .mov, .webm), Primetime Ad Insertion cerca una versione pre-transcodificata dell’annuncio da una specifica CDN. Se ne viene trovata una, l&#39;annuncio è inserito; in caso contrario, l’annuncio viene messo in coda per la transcodifica.

1. Una volta transcodificato il contenuto creativo dell’annuncio, Primetime Ad Insertion unirà tutte le richieste successive per tale risorsa pubblicitaria nei manifesti.

Primetime Ad Insertion supporta la transcodifica per la maggior parte dei formati video e lineari. La transcodifica creativa degli annunci si verifica in genere in meno di tre minuti. Per ulteriori informazioni, contatta il rappresentante di supporto Primetime .
