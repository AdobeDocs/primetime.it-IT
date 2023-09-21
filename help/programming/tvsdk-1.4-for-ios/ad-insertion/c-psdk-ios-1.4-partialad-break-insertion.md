---
description: TVSDK offre un’esperienza simile alla TV, ovvero la possibilità di partecipare nel mezzo di un annuncio in streaming live.
title: Inserimento parziale di interruzione pubblicitaria
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Inserimento parziale di interruzione pubblicitaria{#partial-ad-break-insertion}

TVSDK offre un’esperienza simile alla TV, ovvero la possibilità di partecipare nel mezzo di un annuncio in streaming live.

La funzione di inserimento parziale dell’interruzione pubblicitaria consente di simulare un’esperienza simile a quella TV in cui, se il client avvia uno streaming live all’interno di un mid-roll, inizia la riproduzione all’interno di tale mid-roll. È simile al passaggio a un canale TV e gli spot vengono eseguiti senza problemi.

Ad esempio, se un utente si unisce nel mezzo di un’interruzione pubblicitaria di 90 secondi (tre annunci di 30 secondi), 10 secondi nel secondo annuncio (ovvero, a 40 secondi nell’interruzione pubblicitaria), il secondo annuncio viene riprodotto per la durata rimanente (20 secondi) seguito dal terzo annuncio.

## Tracciamento annuncio {#section_03AFAEAA8DA44399952DC51C5E12951E}

I tracker degli annunci per l’annuncio parzialmente riprodotto (il secondo annuncio) non vengono attivati. Nell’esempio precedente, viene attivato solo il tracker per il terzo annuncio.

## Comportamento con pre-roll {#section_7DFBFB12E63343D1A0C614F0CF9F1714}

Questa funzione funziona quando un annuncio pre-roll viene riprodotto con contenuti live. Il flusso viene riprodotto dal punto live dopo la fine dell’annuncio pre-roll.

Gli eventi di interruzione pubblicitaria vengono inviati anche se non ci sono annunci completi in questa interruzione pubblicitaria. Un annuncio viene considerato parziale se viene saltato per più di un secondo. Ad esempio, se un visualizzatore guarda un annuncio che ha saltato per 800 ms, viene considerato come un annuncio completo.
