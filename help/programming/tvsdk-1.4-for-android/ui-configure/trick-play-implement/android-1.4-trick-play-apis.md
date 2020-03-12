---
description: TVSDK include metodi, proprietà ed eventi per determinare percentuali valide, tassi correnti, se è supportata la riproduzione di trucco e altre funzionalità correlate a avanzamento rapido e riavvolgimento.
seo-description: TVSDK include metodi, proprietà ed eventi per determinare percentuali valide, tassi correnti, se è supportata la riproduzione di trucco e altre funzionalità correlate a avanzamento rapido e riavvolgimento.
seo-title: Elementi API Rate-change
title: Elementi API Rate-change
uuid: 0040d35c-f9cb-4066-9bee-828ed5541194
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Elementi API Rate-change{#rate-change-api-elements}

TVSDK include metodi, proprietà ed eventi per determinare percentuali valide, tassi correnti, se è supportata la riproduzione di trucco e altre funzionalità correlate a avanzamento rapido e riavvolgimento.

<!--<a id="section_36576E92DE6343AEBD0BBD662502365D"></a>-->

Utilizzate i seguenti elementi API per modificare le percentuali di riproduzione:

* `PlaybackRateEvent.getRate`
* `MediaPlayer.getLocalTime`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.getAvailablePlaybackRates` - specifica le tariffe valide.

| Valore rate | Effetto sulla riproduzione |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Passa alla modalità di avanzamento rapido con il moltiplicatore specificato più veloce del normale (ad esempio, 4 è 4 volte più veloce del normale) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Passa alla modalità di riavvolgimento rapido |
| 1.0 | Passa alla modalità di riproduzione normale (la chiamata `play` equivale a impostare la proprietà rate su 1.0) |
| 0.0 | Pause (la chiamata `pause` è la stessa dell&#39;impostazione della proprietà rate su 0.0) |

