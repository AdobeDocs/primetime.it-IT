---
description: TVSDK fornisce un'esperienza simile a quella della TV per partecipare nel mezzo di un annuncio, in streaming live.
seo-description: TVSDK fornisce un'esperienza simile a quella della TV per partecipare nel mezzo di un annuncio, in streaming live.
seo-title: Inserimento parziale degli annunci
title: Inserimento parziale degli annunci
uuid: 799acdd8-fbb9-43b4-955a-3f56825d1e87
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Inserimento parziale degli annunci {#partial-ad-break-insertion}

TVSDK fornisce un&#39;esperienza simile a quella della TV per partecipare nel mezzo di un annuncio, in streaming live.

La funzione di inserimento parziale ad-break consente di riprodurre un&#39;esperienza simile a quella TV, dove, se il client avvia uno streaming live all&#39;interno di un mid-roll, la riproduzione inizia all&#39;interno di quel mid-roll. È simile al passaggio a un canale TV e la pubblicità funziona senza problemi.

Ad esempio, se un utente si unisce nel mezzo di un annuncio di 90 secondi (tre annunci da 30 secondi), 10 secondi alla seconda pubblicità (ovvero, a 40 secondi dall&#39;interruzione dell&#39;annuncio), il secondo annuncio viene riprodotto per la durata rimanente (20 secondi) seguita dal terzo annuncio.

## Track Ad {#section_03AFAEAA8DA44399952DC51C5E12951E}

I tracciatori di annunci per l&#39;annuncio parzialmente riprodotto (il secondo annuncio) non vengono attivati. Nell&#39;esempio precedente, viene attivato solo il tracciatore per il terzo annuncio.

## Comportamento con pre-roll {#section_7DFBFB12E63343D1A0C614F0CF9F1714}

La funzione funziona quando un annuncio pre-roll viene riprodotto con contenuto live. Il flusso viene riprodotto dal punto vivo dopo la fine degli annunci pre-roll.

Gli eventi di interruzione annuncio vengono inviati anche se non ci sono annunci completi in questa interruzione annuncio. Un annuncio è considerato parziale, se viene saltato per più di un secondo. Ad esempio, se un visualizzatore guarda un annuncio che ha saltato per 800 ms, viene considerato come un annuncio completo.