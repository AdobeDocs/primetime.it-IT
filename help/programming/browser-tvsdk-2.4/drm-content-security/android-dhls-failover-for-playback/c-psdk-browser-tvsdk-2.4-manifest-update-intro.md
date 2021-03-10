---
description: Il browser TVSDK può rilevare le informazioni sulla riproduzione modificate nei manifesti master m3u8 per lo streaming live e aggiornare le informazioni sulla riproduzione durante la riproduzione del flusso. Il browser TVSDK supporta un set dinamico di profili a bit rate quando i profili appaiono o scompaiono dal manifest, inclusi i bit rate di profilo non sovrapposti tra gli aggiornamenti.
title: Aggiornamento del master-manifest live
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Aggiornamento del manifesto master live{#live-master-manifest-update}

Il browser TVSDK può rilevare le informazioni sulla riproduzione modificate nei manifesti master m3u8 per lo streaming live e aggiornare le informazioni sulla riproduzione durante la riproduzione del flusso. Il browser TVSDK supporta un set dinamico di profili a bit rate quando i profili appaiono o scompaiono dal manifest, inclusi i bit rate di profilo non sovrapposti tra gli aggiornamenti.

Sono supportate le seguenti funzioni:

* Numero di profili (in aumento o in diminuzione)
* Bit rate del profilo (sovrapposizione o meno)
* Profili con URL sullo stesso server (o su server diversi)
* Qualsiasi struttura di failover

Devono essere soddisfatte tutte le seguenti condizioni:

* Il flusso è live.
* Sia il tempo che il tag cambiano.
* Tutte le informazioni sul rendering rimangono le stesse (tranne che gli URL possono variare).
* Le informazioni di accesso DRM rimangono le stesse.
* I segmenti vengono assemblati intorno agli stessi PTS e i bordi dei fotogrammi in un piccolo intervallo di errore.

