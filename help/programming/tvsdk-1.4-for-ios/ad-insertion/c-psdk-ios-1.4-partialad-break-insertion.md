---
description: TVSDK fornisce un’esperienza simile alla TV di poter partecipare nel mezzo di un annuncio, in flussi live.
title: Inserimento di interruzioni pubblicitarie parziali
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Inserimento di interruzioni pubblicitarie parziali{#partial-ad-break-insertion}

TVSDK fornisce un’esperienza simile alla TV di poter partecipare nel mezzo di un annuncio, in flussi live.

La funzione di inserimento parziale dell’annuncio consente di imitare un’esperienza simile a quella televisiva in cui, se il cliente avvia un flusso live all’interno di un mid-roll, inizia a riprodurre all’interno di quel mid-roll. È simile al passaggio a un canale televisivo e gli spot vengono eseguiti senza problemi.

Ad esempio, se un utente si unisce nel mezzo di un’interruzione pubblicitaria di 90 secondi (tre annunci di 30 secondi), a 10 secondi dal secondo annuncio (cioè a 40 secondi dall’interruzione pubblicitaria), il secondo annuncio viene riprodotto per la durata rimanente (20 secondi) seguita dal terzo annuncio.

## Track Ad {#section_03AFAEAA8DA44399952DC51C5E12951E}

I tracciatori di annunci per l’annuncio parzialmente riprodotto (il secondo annuncio) non vengono attivati. Nell’esempio precedente, viene attivato solo il tracker per il terzo annuncio.

## Comportamento con pre-roll {#section_7DFBFB12E63343D1A0C614F0CF9F1714}

La funzione funziona quando un annuncio pre-roll viene riprodotto con contenuto live. Il flusso viene riprodotto dal punto live dopo la fine degli annunci pre-roll.

Gli eventi di interruzione annuncio vengono inviati anche se non sono presenti annunci completi in questa interruzione annuncio. Un annuncio è considerato parziale, se viene ignorato per più di un secondo. Ad esempio, se un visualizzatore guarda un annuncio che ha saltato per 800 ms, viene considerato come un annuncio completo.
