---
description: Browser TVSDK è in grado di rilevare le modifiche delle informazioni di riproduzione nei manifesti master m3u8 per lo streaming live e aggiornare le informazioni di riproduzione durante la riproduzione del flusso. Browser TVSDK supporta un set dinamico di profili di bitrate man mano che i profili appaiono o scompaiono dal manifest principale, compresi i bitrate di profilo non sovrapposti tra gli aggiornamenti.
seo-description: Browser TVSDK è in grado di rilevare le modifiche delle informazioni di riproduzione nei manifesti master m3u8 per lo streaming live e aggiornare le informazioni di riproduzione durante la riproduzione del flusso. Browser TVSDK supporta un set dinamico di profili di bitrate man mano che i profili appaiono o scompaiono dal manifest principale, compresi i bitrate di profilo non sovrapposti tra gli aggiornamenti.
seo-title: Aggiornamento Live Master-manifest
title: Aggiornamento Live Master-manifest
uuid: 4b918a73-dacf-465a-82d6-404c6bdb01f2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Aggiornamento Live Master-manifest{#live-master-manifest-update}

Browser TVSDK è in grado di rilevare le modifiche delle informazioni di riproduzione nei manifesti master m3u8 per lo streaming live e aggiornare le informazioni di riproduzione durante la riproduzione del flusso. Browser TVSDK supporta un set dinamico di profili di bitrate man mano che i profili appaiono o scompaiono dal manifest principale, compresi i bitrate di profilo non sovrapposti tra gli aggiornamenti.

Sono supportate le seguenti funzionalità:

* Conteggio profili (crescente o decrescente)
* Bitrate del profilo (sovrapposizione o non sovrapposizione)
* Profili con URL sullo stesso server (o su server diversi)
* Qualsiasi struttura di failover

Devono essere soddisfatte tutte le seguenti condizioni:

* Il flusso è live.
* Sia il tempo che il tag cambiano.
* Tutte le informazioni sul rendering rimangono invariate (con la differenza che gli URL possono variare).
* Le informazioni di accesso DRM restano invariate.
* I segmenti sono racchiusi tra gli stessi PTS e i bordi dei fotogrammi in un piccolo intervallo di errore.

