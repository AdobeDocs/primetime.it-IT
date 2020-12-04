---
description: TVSDK include metodi, proprietà ed eventi per determinare percentuali valide, tassi correnti, se è supportata la riproduzione di trucco e altre funzionalità correlate a avanzamento rapido e riavvolgimento.
seo-description: TVSDK include metodi, proprietà ed eventi per determinare percentuali valide, tassi correnti, se è supportata la riproduzione di trucco e altre funzionalità correlate a avanzamento rapido e riavvolgimento.
seo-title: Elementi API Rate-change
title: Elementi API Rate-change
uuid: 3554bf45-9419-4740-8a0e-484fc14c7436
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 2%

---


# Elementi API Rate Change {#rate-change-api-elements}

TVSDK include metodi, proprietà ed eventi per determinare percentuali valide, tassi correnti, se è supportata la riproduzione di trucco e altre funzionalità correlate a avanzamento rapido e riavvolgimento.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

Utilizzate i seguenti elementi API per modificare le percentuali di riproduzione:

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`, che specifica le tariffe valide.

| Valore rate | Effetto sulla riproduzione |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Passa alla modalità di avanzamento rapido con il moltiplicatore specificato più veloce del normale (ad esempio, 4 è 4 volte più veloce del normale) |
| -2,0, -4,0, -8,0, -16,0, -32,0, -64,0, -128,0 | Passa alla modalità di riavvolgimento rapido |
| 1,0 | Passa alla modalità di riproduzione normale (la chiamata di `play` equivale a impostare la proprietà rate su 1.0) |
| 0,0 | Pauses (la chiamata di `pause` equivale all&#39;impostazione della proprietà rate su 0.0) |

