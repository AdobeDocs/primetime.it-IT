---
description: La funzione PABI (Partial Ad Break Insertion) imita un'esperienza simile a quella di un televisore in cui se l'utente partecipa a un flusso live in un'interruzione intermedia, l'utente riceve gli annunci mid-roll invece di un annuncio pre-roll o un'ardesia.
seo-description: La funzione PABI (Partial Ad Break Insertion) imita un'esperienza simile a quella di un televisore in cui se l'utente partecipa a un flusso live in un'interruzione intermedia, l'utente riceve gli annunci mid-roll invece di un annuncio pre-roll o un'ardesia.
seo-title: Inserimento interruzione annuncio parziale
title: Inserimento interruzione annuncio parziale
uuid: a0c1ae34-0f8d-4401-97fe-45a2ea40d08d
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Inserimento interruzione annuncio parziale {#partial-ad-break-insertion}

La funzione PABI (Partial Ad Break Insertion) imita un&#39;esperienza simile a quella di un televisore in cui se l&#39;utente partecipa a un flusso live in un&#39;interruzione intermedia, l&#39;utente riceve gli annunci mid-roll invece di un annuncio pre-roll o un&#39;ardesia.

Quando il server annunci restituisce annunci pre-roll per un flusso live, il server manifesto inserisce l&#39;interruzione annuncio pre-roll prima del punto attivo e inserisce il tag EXT-X-START con il valore TIMEOFFSET che indica l&#39;inizio dell&#39;interruzione annuncio pre-roll. Questo comportamento predefinito assicura che l&#39;intera interruzione dell&#39;annuncio pre-roll venga riprodotta prima del contenuto in un punto attivo. Se un utente si unisce a un flusso quando il punto di attivazione è vicino a un&#39;interruzione annuncio in fase di rollio medio, all&#39;utente verrà mostrata l&#39;interruzione annuncio in fase di pre-roll prima dell&#39;interruzione annuncio in fase di mid-roll al punto di attivazione.

La funzione PABI indica al server del manifesto di ignorare l&#39;interruzione dell&#39;annuncio pre-roll e impostare il valore EXT-X-START:TIMEOFFSET all&#39;inizio del mid-roll e presente al live-point. Questo garantisce che l&#39;utente visualizzi l&#39;intero annuncio mid-roll in fase di riproduzione al punto attivo senza dover visualizzare l&#39;annuncio pre-roll.

>[!NOTE]
>
>Questa funzionalità è disponibile solo per i flussi live. Per impostazione predefinita, il server del manifesto inserisce l’interruzione dell’annuncio pre-roll nella playlist VOD.

>[!NOTE]
>
>Per abilitare PABI, dovrete specificare [query_params](../../msapi-topics/ms-getting-started/ms-api-query-params.md) nell&#39;URL del programma di avvio.

>[!NOTE]
>
>Il [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) è un tag HLS standard che indica un punto iniziale preferito all&#39;interno della playlist.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* Utilizzate il tracciamento lato client perché il client ha maggiore controllo sull&#39;attivazione dei beacon di tracciamento.
* Le interruzioni pubblicitarie parziali devono essere utilizzate con la modalità di tracciamento lato server solo se il lettore supporta EXT-X-START.