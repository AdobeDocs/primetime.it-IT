---
title: Risoluzione dei problemi e debug
description: Risoluzione dei problemi e debug
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Risoluzione dei problemi e debug {#troubleshooting-debugging}

Primetime Ad Insertion offre strumenti per identificare e diagnosticare i problemi che possono verificarsi in tutte le fasi della distribuzione del video, ad esempio errori di consegna CDN, errori di creazione pubblicitaria o errori di connettività client.

Primetime Ad Insertion supporta la registrazione dettagliata tramite [Bootstrap parametro API](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md) `ptdebug=true` o `ptdebug=AdCall` all&#39;URL di avvio. I registri vengono inviati sia alle intestazioni di risposta HTTP che alla console Ad Insertion di Primetime. Questo parametro è destinato solo ai test localizzati, non ai flussi di produzione. Per ulteriori informazioni sui tipi di messaggio quando è abilitata la registrazione dettagliata, consulta [eventi di registrazione ptdebug in registrazione dettagliata](verbose-logging.md#ptdebug-logging-events).

Primetime Ad Insertion fornisce anche il debug delle prestazioni su tutte le richieste con l’intestazione X-ADBE-AI-X1, che può essere utilizzata per misurare le prestazioni e gli inserimenti di annunci su qualsiasi richiesta. Questa intestazione di richiesta è disponibile indipendentemente dal fatto che la registrazione dettagliata sia abilitata o meno. Per ulteriori informazioni, consulta [Intestazioni dettagliate: X-ADBE-PTAI-X1](debugging-headers.md).
