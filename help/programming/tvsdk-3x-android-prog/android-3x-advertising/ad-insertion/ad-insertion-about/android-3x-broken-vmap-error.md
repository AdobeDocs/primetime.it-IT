---
description: Quando TVSDK rileva un VMAP interrotto in una risposta ad server, invia un errore 1109 (NETWORK_AD_URL_FAILED).
keywords: 1109;NETWORK_AD_URL_FAILED;VMAP interrotto
title: Gestione degli errori client per VMAP non funzionante
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Gestione degli errori client per VMAP non funzionante {#client-error-handling-for-broken-vmap}

Quando TVSDK rileva un VMAP interrotto in una risposta ad server, invia un errore 1109 (NETWORK_AD_URL_FAILED).

A seconda della natura della risposta del server di annunci e delle impostazioni di caricamento degli annunci, il lettore potrebbe ricevere numeri diversi di errori 1109 quando TVSDK incontra un VMAP non funzionante in una risposta del server di annunci.

Consideriamo uno scenario in cui la risposta del server di annunci punta a VMAP XML. Diciamo anche che la risposta ad server ha quattro slot per annunci disponibili, ciascuno dei quali punta allo stesso VMAP. Infine, diciamo che questo VMAP è rotto.

In questo scenario, se la risoluzione degli annunci pigri è abilitata ([Abilita risoluzione annunci pigri](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)), TVSDK invierà due errori 1109 (non uno come previsto): viene inviato un errore su ogni passaggio di analisi sulla timeline. Questo perché quando la risoluzione degli annunci pigri è abilitata, TVSDK analizza gli annunci in 2 passaggi: la prima passata avviene immediatamente prima dell’avvio della riproduzione dei contenuti per gli annunci pre-scorrimento, e la seconda passata avviene dopo l’avvio della riproduzione, per gli annunci mid-roll e post-roll.

>[!NOTE]
>
>In questo scenario, se disattivi la risoluzione lenta degli annunci, TVSDK attiverà un solo errore 1109 (un solo passaggio di analisi).