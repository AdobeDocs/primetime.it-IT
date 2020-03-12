---
description: Per consentire ai clienti che desiderano pagare solo ciò che utilizzano, anziché un tasso fisso indipendentemente dall'uso effettivo, Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.
seo-description: Per consentire ai clienti che desiderano pagare solo ciò che utilizzano, anziché un tasso fisso indipendentemente dall'uso effettivo, Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.
seo-title: Metriche di fatturazione
title: Metriche di fatturazione
uuid: 4a03995a-60f6-440e-9cdf-9c0b9c5f1d90
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Panoramica {#billing-metrics-overview}

Per consentire ai clienti che desiderano pagare solo ciò che utilizzano, anziché un tasso fisso indipendentemente dall&#39;uso effettivo, Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.

Ogni volta che il lettore genera un evento di avvio del flusso, TVSDK inizia a inviare periodicamente messaggi HTTP al sistema di fatturazione di Adobe. Il periodo, noto come durata fatturabile, può essere diverso per VOD standard, pro VOD (annunci mid-roll abilitati) e contenuti live. La durata predefinita di ciascun tipo di contenuto è di 30 minuti, ma il contratto con Adobe determina i valori effettivi.

I messaggi contengono le informazioni seguenti:

* Tipo di contenuto (live, lineare o VOD)
* URL contenuto
* Se gli annunci pubblicitari sono abilitati
* Se gli annunci mid-roll sono abilitati (solo VOD)
* Se il flusso è protetto da DRM
* La versione e la piattaforma TVSDK

Adobe preconfigura questa disposizione, ma potete collaborare con il rappresentante di Adobe Enablement per modificarla e collaborare con il rappresentante di Adobe Enablement.

Per monitorare le statistiche inviate da TVSDK ad Adobe, ottenere l’URL dal rappresentante Adobe Enablement e utilizzare uno strumento di acquisizione di rete, come Charles, per visualizzare i dati.
