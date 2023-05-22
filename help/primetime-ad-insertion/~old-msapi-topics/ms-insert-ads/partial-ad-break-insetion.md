---
description: La funzione PABI (Partial Ad Break Insertion) simula un’esperienza simile a quella televisiva in cui, se l’utente unisce uno streaming live all’interno di un’interruzione mid-roll, vengono visualizzati annunci mid-roll invece di un annuncio pre-roll o di uno slate.
title: Inserimento interruzione pubblicitaria parziale
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Inserimento interruzione pubblicitaria parziale {#partial-ad-break-insertion}

La funzione PABI (Partial Ad Break Insertion) simula un’esperienza simile a quella televisiva in cui, se l’utente unisce uno streaming live all’interno di un’interruzione mid-roll, vengono visualizzati annunci mid-roll invece di un annuncio pre-roll o di uno slate.

Quando il server di annunci restituisce annunci pre-roll per un flusso live, il server di manifesto inserisce l’interruzione pubblicitaria pre-roll prima del punto live e inserisce il tag EXT-X-START con il relativo valore TIMEOFFSET che punta all’inizio dell’interruzione pubblicitaria pre-roll. Questo comportamento predefinito assicura che l’intera interruzione pubblicitaria pre-roll venga riprodotta prima del contenuto in corrispondenza del punto di attivazione. Se un utente si unisce a un flusso quando il punto di attivazione è vicino a un’interruzione pubblicitaria mid-roll, all’utente verrà mostrata l’interruzione pubblicitaria pre-roll prima dell’interruzione pubblicitaria mid-roll al punto di attivazione.

La funzione PABI indica al server manifesto di ignorare l&#39;interruzione pubblicitaria pre-roll e di impostare il valore EXT-X-START:TIMEOFFSET all&#39;inizio dell&#39;annuncio mid-roll presente al punto di attivazione. In questo modo l’utente può vedere l’intero annuncio mid-roll attualmente riprodotto dal vivo senza dover visualizzare l’interruzione pubblicitaria pre-roll.

>[!NOTE]
>
>Questa funzionalità è disponibile solo per i flussi live. Per impostazione predefinita, il server manifest inserisce l’interruzione pubblicitaria pre-roll in cima alla playlist VOD.

>[!NOTE]
>
>Per attivare PABI, è necessario specificare [query_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) nell&#39;URL di avvio.

>[!NOTE]
>
>Il [INT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) è un tag HLS standard che indica un punto di partenza preferito all’interno della playlist.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* Utilizza il tracciamento lato client perché il client ha un maggiore controllo sull&#39;attivazione dei beacon di tracciamento.
* Le interruzioni pubblicitarie parziali devono essere utilizzate solo con la modalità di tracciamento lato server se il lettore supporta EXT-X-START.