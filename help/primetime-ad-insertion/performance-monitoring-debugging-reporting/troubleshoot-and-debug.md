---
title: Risoluzione dei problemi e debug
description: Risoluzione dei problemi e debug
copied-description: true
exl-id: 1fcacd29-627d-4536-a746-16ddcfc8bc34
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Risolvere i problemi ed eseguire il debug {#troubleshooting-debugging}

Primetime Ad Insertion offre strumenti per identificare e diagnosticare i problemi che possono verificarsi in tutte le fasi della distribuzione video, ad esempio errori di consegna CDN, errori creativi o errori di connettività del client.

Primetime Ad Insertion supporta la registrazione dettagliata tramite il [parametro API Bootstrap](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` o `ptdebug=AdCall` all&#39;URL di avvio. I registri vengono inviati sia alle intestazioni di risposta HTTP che alla console Primetime Ad Insertion. Questo parametro è destinato solo ai test localizzati, non ai flussi di produzione. Per ulteriori informazioni sui tipi di messaggi quando la registrazione dettagliata è abilitata, consulta [eventi di registrazione ptdebug in registrazione dettagliata](verbose-logging.md#ptdebug-logging-events).

Primetime Ad Insertion fornisce anche il debug delle prestazioni su tutte le richieste con l&#39;intestazione X-ADBE-AI-X1, che può essere utilizzato per misurare le prestazioni e gli inserimenti di annunci su qualsiasi richiesta specifica. Questa intestazione di richiesta è disponibile indipendentemente dal fatto che la registrazione dettagliata sia abilitata. Per ulteriori informazioni, consulta [Intestazioni dettagliate: X-ADBE-PTAI-X1](debugging-headers.md).
