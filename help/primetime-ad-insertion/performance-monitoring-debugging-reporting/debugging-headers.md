---
title: Intestazioni di debug
description: Intestazioni di debug
copied-description: true
exl-id: 42c19089-2c61-4622-b53a-c28b8d495ef8
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---

# Intestazioni di debug (X-ADBE-AI-X1) {#debugging-headers}

SSAI invia intestazioni HTTP che possono essere utilizzate per raccogliere informazioni e determinare le prestazioni per le sessioni di produzione, che si trovano nell&#39;intestazione X-ADBE-AI-X1.

Intestazione di esempio:
`X-ADBE-AI-X1: 0 1 1594181097704 15126333-5ba9-49b8-a219-4f37e60d259c v 0 1 30 2 1 199 2 185 497 204 104 0 1 0 4`

La descrizione dei campi è la seguente:

| Nome | Descrizione | Esempio |
|--- |--- |--- |
| isActivePreroll | Se è stata inviata una chiamata ad per pre-roll | 0 |
| isActiveMidroll | Se è stata inviata una chiamata ad per midroll-roll | 3 |
| ID richiesta | SSAI interno | 1594181097704 |
| ID sessione | ID sessione della richiesta | 1512633-5ba9-49b8-a219-4f37e60d259c |
| Tipo di flusso | u=variante, l=live, v=vod | v |
| isBootstrap | Se questa richiesta è una chiamata di avvio | 0 |
| Conteggio interruzioni annunci | Numero totale di interruzioni pubblicitarie nel manifesto | 3 |
| Durata totale dell’interruzione dell’annuncio | Durata totale dell’interruzione pubblicitaria, in secondi | 30 |
| Conteggio chiamate annunci | Numero di chiamate ad inviate nella richiesta | 2 |
| Conteggio chiamate ad reindirizzamento | Numero di chiamate ad di reindirizzamento inviate nella richiesta | 1 |
| Durata totale della chiamata dell’annuncio | Tempo di elaborazione totale delle chiamate ad | 199 |
| Conteggio annunci inserito | Numero di annunci inseriti nel manifesto | 2 |
| Tempo di richiesta del manifesto di origine | Tempo impiegato solo per il recupero del contenuto | 185 |
| Tempo di richiesta totale | Tempo totale impiegato per recuperare contenuti e annunci | 497 |
| Tempo di recupero manifesto dell’annuncio (totale) | Quantità totale di annunci pubblicitari da recuperare | 204 |
| Tempo di recupero manifesto dell’annuncio (effettivo) | Quantità effettiva di eventi di recupero annunci in parallelo | 104 |
| Hit nella cache dei contenuti | Numero di hit della cache del contenuto | 0 |
| Mancanza nella cache del contenuto | Numero di mancati riscontri nella cache del contenuto | 3 |
| Hit cache manifesto dell&#39;annuncio | Numero di hit della cache del manifesto di annunci | 0 |
| Mancata cache manifesto dell’annuncio | Numero di mancati riscontri nella cache del manifesto dell&#39;annuncio | 4 |
