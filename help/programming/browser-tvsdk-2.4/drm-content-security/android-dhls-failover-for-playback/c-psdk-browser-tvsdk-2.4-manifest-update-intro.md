---
description: Il browser TVSDK può rilevare le informazioni di riproduzione modificate nei manifesti master m3u8 per lo streaming live e aggiornare le informazioni di riproduzione durante la riproduzione del flusso. Il TVSDK del browser supporta un set dinamico di profili di velocità in bit quando i profili appaiono o scompaiono dal manifesto principale, incluse velocità in bit di profilo non sovrapposte tra gli aggiornamenti.
title: Aggiornamento Live master-manifesto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Aggiornamento Live master-manifesto{#live-master-manifest-update}

Il browser TVSDK può rilevare le informazioni di riproduzione modificate nei manifesti master m3u8 per lo streaming live e aggiornare le informazioni di riproduzione durante la riproduzione del flusso. Il TVSDK del browser supporta un set dinamico di profili di velocità in bit quando i profili appaiono o scompaiono dal manifesto principale, incluse velocità in bit di profilo non sovrapposte tra gli aggiornamenti.

Sono supportate le seguenti funzionalità:

* Conteggio profili (crescente o decrescente)
* Velocità in bit del profilo (sovrapposizione o non sovrapposizione)
* Profili con URL sugli stessi server (o su server diversi)
* Qualsiasi struttura di failover

Devono essere soddisfatte tutte le seguenti condizioni:

* Il flusso è live.
* Cambiano sia l’ora che l’e-mail.
* Tutte le informazioni sulla rappresentazione rimangono invariate, tranne che gli URL possono variare.
* Le informazioni di accesso DRM rimangono invariate.
* I segmenti sono raggruppati intorno allo stesso PTS e ai limiti del frame in un intervallo di errori ridotto.
