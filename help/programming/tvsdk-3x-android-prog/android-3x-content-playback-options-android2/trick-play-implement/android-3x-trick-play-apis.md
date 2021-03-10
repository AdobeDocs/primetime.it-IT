---
description: TVSDK include metodi, proprietà ed eventi per determinare le percentuali valide, le percentuali correnti, se è supportata la riproduzione per trucco e altre funzionalità correlate alla riavvolgimento e all’avanzamento rapido.
title: Elementi API per la modifica dei tassi
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---


# Elementi API di modifica della velocità {#rate-change-api-elements}

TVSDK include metodi, proprietà ed eventi per determinare le percentuali valide, le percentuali correnti, se è supportata la riproduzione per trucco e altre funzionalità correlate alla riavvolgimento e all’avanzamento rapido.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

Utilizza i seguenti elementi API per modificare le percentuali di riproduzione:

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`, che specifica le percentuali valide.

| **Valore rate** | **Effetto sulla riproduzione** |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Passa alla modalità di avanzamento rapido con il moltiplicatore specificato più rapidamente del normale (ad esempio, 4 è 4 volte più veloce del normale) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Passa alla modalità di riavvolgimento rapido |
| 1,0 | Passa alla modalità di riproduzione normale (chiamare `play` equivale a impostare la proprietà rate su 1.0) |
| 0,0 | Sospensioni (la chiamata di `pause` equivale all&#39;impostazione della proprietà rate su 0.0) |