---
description: TVSDK include metodi, proprietà ed eventi per determinare i tassi validi, i tassi correnti, se è supportata la riproduzione con trucco e altre funzionalità correlate all'avanzamento e al riavvolgimento rapido.
title: Elementi API per la modifica della velocità
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# Elementi API per la modifica della velocità {#rate-change-api-elements}

TVSDK include metodi, proprietà ed eventi per determinare i tassi validi, i tassi correnti, se è supportata la riproduzione con trucco e altre funzionalità correlate all&#39;avanzamento e al riavvolgimento rapido.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

Utilizza i seguenti elementi API per modificare le percentuali di riproduzione:

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`, che specifica tariffe valide.

| Valore tariffa | Effetto sulla riproduzione |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Passa alla modalità di avanzamento rapido con il moltiplicatore specificato più rapidamente del normale (ad esempio, 4 è 4 volte più veloce del normale) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Passa alla modalità di riavvolgimento rapido |
| 1.0 | Passa alla modalità di riproduzione normale (chiamata `play` equivale a impostare la proprietà rate su 1,0) |
| 0.0 | Pause (chiamata `pause` equivale a impostare la proprietà rate su 0,0) |
