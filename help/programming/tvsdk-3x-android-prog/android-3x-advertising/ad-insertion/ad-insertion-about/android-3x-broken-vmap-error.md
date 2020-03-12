---
description: Quando TVSDK rileva un elemento VMAP danneggiato in una risposta del server di annunci, invia un errore 1109 (NETWORK_AD_URL_FAILED).
keywords: 1109;NETWORK_AD_URL_FAILED;broken VMAP
seo-description: Quando TVSDK rileva un elemento VMAP danneggiato in una risposta del server di annunci, invia un errore 1109 (NETWORK_AD_URL_FAILED).
seo-title: Gestione errori client per VMAP interrotto
title: Gestione errori client per VMAP interrotto
uuid: ab2c567d-d945-4ebe-b65a-c1f13518a576
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Gestione errori client per VMAP interrotto {#client-error-handling-for-broken-vmap}

Quando TVSDK rileva un elemento VMAP danneggiato in una risposta del server di annunci, invia un errore 1109 (NETWORK_AD_URL_FAILED).

A seconda della natura della risposta del server di annunci e delle impostazioni di caricamento degli annunci, il lettore potrebbe ricevere numeri diversi di errori 1109 quando TVSDK rileva un VMAP guasto in una risposta del server di annunci.

Consideriamo uno scenario in cui la risposta del server di annunci punta a VMAP XML. Supponiamo anche che la risposta del server di annunci ha quattro slot pubblicitari disponibili, ciascuno dei quali punta allo stesso VMAP. Infine, diciamo che questo VMAP è rotto.

In questo scenario, se la risoluzione degli annunci pigri è abilitata ([Abilita risoluzione](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)annunci pigri), TVSDK invierà due errori 1109 (non uno come previsto): viene inviato un errore su ogni passaggio di analisi sulla timeline. Questo perché quando la risoluzione degli annunci pigri è abilitata, TVSDK analizza gli annunci in 2 passaggi: la prima passata avviene immediatamente prima dell&#39;inizio della riproduzione del contenuto per gli annunci pre-roll, e la seconda passata avviene dopo l&#39;avvio della riproduzione, per gli annunci mid-roll e post-roll.

>[!NOTE]
>
>In questo scenario, se disattivi la risoluzione degli annunci pigri, TVSDK genererà un solo errore 1109 (solo un passaggio di analisi).