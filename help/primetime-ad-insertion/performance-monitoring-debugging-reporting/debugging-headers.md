---
title: Eseguire il debug delle intestazioni
description: Eseguire il debug delle intestazioni
copied-description: true
exl-id: 42c19089-2c61-4622-b53a-c28b8d495ef8
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---

# Debug delle intestazioni (X-ADBE-AI-X1) {#debugging-headers}

SSAI invia intestazioni HTTP che possono essere utilizzate per raccogliere informazioni e determinare le prestazioni per le sessioni di produzione, che si trovano nell&#39;intestazione X-ADBE-AI-X1.

Esempio di intestazione:
`X-ADBE-AI-X1: 0 1 1594181097704 15126333-5ba9-49b8-a219-4f37e60d259c v 0 1 30 2 1 199 2 185 497 204 104 0 1 0 4`

La descrizione dei campi è la seguente:

| Nome | Descrizione | Esempio |
|--- |--- |--- |
| isActivePreroll | Se è stata inviata una chiamata annuncio per pre-roll | 0 |
| isActiveMidroll | Se è stata inviata una chiamata annuncio per midroll-roll | 1 |
| ID richiesta | Interno SSAI | 1594181097704 |
| ID sessione | ID sessione della richiesta | 15126333-5ba9-49b8-a219-4f37e60d259c |
| Tipo di flusso | u=variant, l=live, v=vod | v |
| isBootstrap | Se questa richiesta è una chiamata bootstrap | 0 |
| Conteggio interruzioni annuncio | Numero totale di interruzioni pubblicitarie nel manifesto | 1 |
| Durata totale interruzione annuncio | Durata totale dell’interruzione pubblicitaria, in secondi | 30 |
| Conteggio chiamate annuncio | Numero di chiamate di annunci inviate in questa richiesta | 2 |
| Numero di chiamate degli annunci di reindirizzamento | Numero di chiamate di reindirizzamento di annunci inviate in questa richiesta | 1 |
| Durata totale della chiamata dell’annuncio | Tempo totale di elaborazione della chiamata annuncio | 199 |
| Conteggio annunci inseriti | Numero di annunci inseriti nel manifesto | 2 |
| Ora richiesta manifesto sorgente | Tempo impiegato per recuperare solo il contenuto | 185 |
| Tempo totale richiesta | Tempo totale impiegato per recuperare contenuti e annunci | 497 |
| Tempo di recupero del manifesto dell’annuncio (totale) | Tempo totale per il recupero dei manifesti pubblicitari | 204 |
| Tempo di recupero del manifesto dell’annuncio (effettivo) | Quantità effettiva di tempo per il recupero e la visualizzazione in parallelo | 104 |
| Risultati cache contenuto | Numero di hit della cache del contenuto | 0 |
| Cache contenuto non trovata | Numero di mancati riscontri nella cache del contenuto | 1 |
| Hit cache manifesto annuncio | Numero di riscontri nella cache del manifesto dell’annuncio | 0 |
| Mancato riscontro nella cache del manifesto dell’annuncio | Numero di mancati riscontri nella cache del manifesto dell’annuncio | 4 |
