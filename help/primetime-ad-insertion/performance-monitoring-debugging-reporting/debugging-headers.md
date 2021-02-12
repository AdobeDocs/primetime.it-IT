---
title: Debugging delle intestazioni
description: null
translation-type: tm+mt
source-git-commit: 45e5c8e6144adf4a405bde7d8d19505b7ad549e0
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 7%

---


# Debugging delle intestazioni (X-ADBE-AI-X1) {#debugging-headers}

SSAI invia intestazioni HTTP utilizzabili per raccogliere informazioni e determinare le prestazioni per le sessioni di produzione, che si trovano nell’intestazione X-ADBE-AI-X1.

Intestazione esempio:
`X-ADBE-AI-X1: 0 1 1594181097704 15126333-5ba9-49b8-a219-4f37e60d259c v 0 1 30 2 1 199 2 185 497 204 104 0 1 0 4`

La descrizione dei campi è la seguente:

| Nome | Descrizione | Esempio |
|--- |--- |--- |
| isActivePreroll | Indica se è stata inviata una richiesta di annuncio per pre-roll | 0 |
| isActiveMidroll | Indica se è stata inviata una chiamata ad annuncio per il midroll-roll | 1 |
| ID richiesta | SSAI interno | 1594181097704 |
| ID sessione | ID sessione della richiesta | 15126333-5ba9-49b8-a219-4f37e60d259c |
| Tipo di flusso | u=variante, l=live, v=vod | v |
| isBootstrap | Indica se questa richiesta è una chiamata di avvio | 0 |
| Conteggio interruzioni annuncio | Numero totale di interruzioni pubblicitarie nel manifesto | 1 |
| Durata totale interruzione annuncio | Durata totale dell&#39;interruzione annuncio, in secondi | 30 |
| Conteggio chiamate annuncio | Numero di chiamate ad annunci inviate in questa richiesta | 2 |
| Conteggio chiamate pubblicitarie di reindirizzamento | Numero di chiamate di reindirizzamento ad inviate in questa richiesta | 1 |
| Durata totale chiamate annuncio | Tempo di elaborazione annunci totali | 199 |
| Conteggio annunci inseriti | Numero di annunci inseriti nel manifesto | 2 |
| Tempo richiesta manifesto origine | Tempo impiegato per recuperare solo il contenuto | 185 |
| Tempo totale richiesta | Tempo totale impiegato per recuperare contenuti e annunci | 497 |
| Tempo recupero manifesto annuncio (totale) | Quantità totale di annunci con recupero di tempo | 204 |
| Tempo recupero manifesto annuncio (effettivo) | Quantità effettiva di eventi pubblicitari da recuperare in parallelo | 104 |
| Hit cache contenuto | Numero di hit della cache del contenuto | 0 |
| Mancanza cache contenuto | Numero di errori nella cache del contenuto | 3 |
| Hit cache manifesto annuncio | Numero di hit della cache del manifesto degli annunci | 0 |
| Mancata cache manifesto annuncio | Numero di errori cache del manifesto dell&#39;annuncio | 4 |