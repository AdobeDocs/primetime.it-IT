---
description: La funzione PABI (Partial Ad Break Insertion) imita un’esperienza simile a quella di un televisore in cui, se l’utente partecipa a un flusso live all’interno di un’interruzione di scorrimento intermedio, l’utente riceve annunci di mid-roll invece di un annuncio pre-roll o di un’ardesia.
title: Inserimento di interruzioni pubblicitarie parziali
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Inserimento di interruzioni pubblicitarie parziali {#partial-ad-break-insertion}

La funzione PABI (Partial Ad Break Insertion) imita un’esperienza simile a quella di un televisore in cui, se l’utente partecipa a un flusso live all’interno di un’interruzione di scorrimento intermedio, l’utente riceve annunci di mid-roll invece di un annuncio pre-roll o di un’ardesia.

Quando il server di annunci restituisce annunci pre-roll per un flusso live, il server manifest inserisce l&#39;interruzione dell&#39;annuncio pre-roll prima del punto live e inserisce il tag EXT-X-START con il suo valore TIMEOFFSET che punta all&#39;inizio dell&#39;interruzione dell&#39;annuncio pre-roll. Questo comportamento predefinito assicura che l’intera interruzione pubblicitaria pre-roll venga riprodotta prima del contenuto in corrispondenza del punto attivo. Se un utente accede a un flusso quando il punto attivo è vicino a un’interruzione pubblicitaria a mid-roll, all’utente viene mostrata l’interruzione pubblicitaria pre-roll prima dell’interruzione pubblicitaria mid-roll al punto attivo.

La funzione PABI indica al server manifest di ignorare l&#39;interruzione dell&#39;annuncio pre-roll e di impostare il valore EXT-X-START:TIMEOFFSET all&#39;inizio del mid-roll e presente al punto live. In questo modo l&#39;utente può vedere l&#39;intero annuncio mid-roll attualmente in riproduzione al punto live senza dover visualizzare l&#39;annuncio pre-roll.

>[!NOTE]
>
>Questa funzionalità è disponibile solo per i flussi live. Per impostazione predefinita, il server manifest inserisce la pre-roll ad break nella playlist VOD.

>[!NOTE]
>
>Per abilitare PABI, dovrai specificare il valore [query_params](/help/primetime-ad-insertion/~old-msapi-topics/ms-getting-started/ms-api-query-params.md) nell&#39;URL di avvio.

>[!NOTE]
>
>Il [EXT-X-START](https://tools.ietf.org/html/rfc8216#section-4.3.5.2) è un tag HLS standard che indica un punto iniziale preferito all&#39;interno della playlist.

## Recommendations {#section_4CF0733B14504F2A99690310B9F3B130}

* Utilizza il tracciamento lato client perché il client ha più controllo sull&#39;attivazione dei beacon di tracciamento.
* Le interruzioni pubblicitarie parziali devono essere utilizzate con la modalità di tracciamento lato server solo se il lettore supporta EXT-X-START.