---
description: Quando TVSDK rileva una VMAP interrotta in una risposta di un ad server, invia un errore 1109 (NETWORK_AD_URL_FAILED).
keywords: 1109;NETWORK_AD_URL_FAILED;BREAKED VMAP
title: Gestione degli errori client per VMAP interrotta
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Gestione degli errori client per VMAP interrotta {#client-error-handling-for-broken-vmap}

Quando TVSDK rileva una VMAP interrotta in una risposta di un ad server, invia un errore 1109 (NETWORK_AD_URL_FAILED).

A seconda della natura della risposta dell’ad server e delle impostazioni di caricamento dell’annuncio, il lettore potrebbe ricevere diversi numeri di errori 1109 quando TVSDK rileva una VMAP interrotta in una risposta dell’ad server.

Prendiamo in considerazione uno scenario in cui la risposta dell’ad server punta all’XML VMAP. Supponiamo inoltre che la risposta dell’ad server disponga di quattro slot pubblicitari disponibili, ciascuno dei quali punta alla stessa VMAP. Infine, supponiamo che questa VMAP sia rotta.

In questo scenario, se la risoluzione lenta degli annunci è abilitata ([Abilita lazy ad resolving](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/t-enable-lazy-ad-resolving.md)), TVSDK invierà due errori 1109 (non uno come previsto): viene inviato un errore a ogni passaggio di analisi sulla timeline. Questo perché quando è abilitata la risoluzione lenta degli annunci, TVSDK analizza gli annunci in 2 passaggi: il primo passaggio si verifica appena prima che inizi la riproduzione del contenuto per gli annunci pre-roll e il secondo passaggio si verifica dopo l’avvio della riproduzione, per gli annunci mid-roll e post-roll.

>[!NOTE]
>
>In questo scenario, se disattivi la risoluzione lazy degli annunci, TVSDK attiverà solo un errore 1109 (una sola passata di analisi).
