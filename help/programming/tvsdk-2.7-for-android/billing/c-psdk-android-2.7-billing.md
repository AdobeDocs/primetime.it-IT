---
description: Per ospitare i clienti che desiderano pagare solo per ciò che utilizzano, piuttosto che per un tasso fisso, indipendentemente dall'uso effettivo,  Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.
seo-description: Per ospitare i clienti che desiderano pagare solo per ciò che utilizzano, piuttosto che per un tasso fisso, indipendentemente dall'uso effettivo,  Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.
seo-title: Metriche di fatturazione
title: Metriche di fatturazione
uuid: 4a03995a-60f6-440e-9cdf-9c0b9c5f1d90
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Panoramica {#billing-metrics-overview}

Per ospitare i clienti che desiderano pagare solo per ciò che utilizzano, piuttosto che per un tasso fisso, indipendentemente dall&#39;uso effettivo,  Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.

Ogni volta che il lettore genera un evento di avvio del flusso, TVSDK inizia a inviare messaggi HTTP periodicamente  Adobe  sistema di fatturazione. Il periodo, noto come durata fatturabile, può essere diverso per VOD standard, pro VOD (annunci mid-roll abilitati) e contenuti live. La durata predefinita di ciascun tipo di contenuto è di 30 minuti, ma il contratto con  Adobe determina i valori effettivi.

I messaggi contengono le informazioni seguenti:

* Tipo di contenuto (live, lineare o VOD)
* URL contenuto
* Se gli annunci pubblicitari sono abilitati
* Se gli annunci mid-roll sono abilitati (solo VOD)
* Se il flusso è protetto da DRM
* La versione e la piattaforma TVSDK

 Adobe preconfigura questa disposizione, ma potete collaborare con il rappresentante di abilitazione  Adobe per modificare l&#39;accordo, lavorare con il rappresentante di abilitazione  Adobe.

Per monitorare le statistiche inviate da TVSDK a  Adobe, ottenere l&#39;URL dal rappresentante di abilitazione  Adobe e utilizzare uno strumento di acquisizione di rete, come Charles, per visualizzare i dati.
