---
title: Risoluzione dei problemi e debug
description: null
translation-type: tm+mt
source-git-commit: 242b5a2875ebc0e0020296ce9489dd54438b5ad0
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Risoluzione dei problemi e debug {#troubleshooting-debugging}

Primetime  Ad Insertion offre strumenti per identificare e diagnosticare i problemi che possono verificarsi in tutte le fasi della distribuzione video, come errori di distribuzione CDN, errori creativi o errori di connettività del client.

Primetime  Ad Insertion supporta la registrazione dettagliata tramite il parametro [Bootstrap API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` o `ptdebug=AdCall` all&#39;URL di avvio. I registri vengono inviati sia alle intestazioni di risposta HTTP che alla console Ad Insertion  Primetime. Questo parametro è destinato solo ai test localizzati, non ai flussi di produzione. Per ulteriori informazioni sui tipi di messaggi quando la registrazione dettagliata è abilitata, vedere [eventi di registrazione ptdebug in registro dettagliato](verbose-logging.md#ptdebug-logging-events).

Primetime  Ad Insertion fornisce anche il debug delle prestazioni su tutte le richieste con l&#39;intestazione X-ADBE-AI-X1, che può essere utilizzata per misurare le prestazioni e gli inserimenti di annunci su qualsiasi richiesta. Questa intestazione di richiesta è disponibile indipendentemente dal fatto che sia abilitata o meno la registrazione dettagliata. Per ulteriori informazioni, vedere [Intestazioni dettagliate: X-ADBE-PTAI-X1](debugging-headers.md).
