---
title: Transcodifica just-in-time
description: Transcodifica just-in-time
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Transcodifica just-in-time {#just-in-time-transcoding}

Primetime Ad Insertion offre funzionalità di transcodifica e creazione di pacchetti just-in-time per garantire la corretta riproduzione di contenuti incompatibili. Può anche inserire pacchetti ID3 in frammenti di annunci che possono essere utilizzati nel tracciamento degli annunci lato client.
Un flusso di lavoro tipico è il seguente:

1. Adobe Primetime Ad Insertion recupera annunci/creativi dal server di annunci del cliente.

1. Se il formato creativo di un annuncio è compatibile in modo nativo con il flusso di contenuto, la creatività viene inserita nel manifesto.

1. Se il formato creativo di un annuncio non è compatibile in modalità nativa (ad esempio, .mp4, .mov, .webm), l’Ad Insertion di Primetime cerca una versione pretranscodificata dell’annuncio da una rete CDN specificata. Se ne viene trovato uno, l’annuncio viene inserito; in caso contrario, l’annuncio viene inserito nella coda per la trascodifica.

1. Dopo che la creatività dell’annuncio è stata transcodificata, Primetime Ad Insertion unirà tutte le richieste successive per tale risorsa annuncio nei manifesti.

Primetime Ad Insertion supporta la transcodifica per la maggior parte dei formati video e lineari. La transcodifica creativa degli annunci si verifica in genere in meno di tre minuti. Per ulteriori informazioni, contatta il rappresentante dell’assistenza Primetime.
