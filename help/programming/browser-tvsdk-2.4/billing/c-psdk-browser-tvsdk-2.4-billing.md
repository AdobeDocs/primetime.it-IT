---
description: Per ospitare i clienti che desiderano pagare solo per ciò che utilizzano, piuttosto che per un tasso fisso, indipendentemente dall'uso effettivo,  Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.
seo-description: Per ospitare i clienti che desiderano pagare solo per ciò che utilizzano, piuttosto che per un tasso fisso, indipendentemente dall'uso effettivo,  Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.
seo-title: Metriche di fatturazione
title: Metriche di fatturazione
uuid: e09b77b3-89d3-44d6-be4e-e1612fbf89fc
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Panoramica {#billing-metrics-overview}

Per ospitare i clienti che desiderano pagare solo per ciò che utilizzano, piuttosto che per un tasso fisso, indipendentemente dall&#39;uso effettivo,  Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto addebitare ai clienti.

Ogni volta che il lettore genera un evento di avvio del flusso, Browser TVSDK inizia a inviare messaggi HTTP periodicamente  Adobe  sistema di fatturazione. Il periodo, noto come durata fatturabile, può essere diverso per VOD standard, pro VOD (annunci mid-roll abilitati) e contenuti live. La durata predefinita di ciascun tipo di contenuto è di 30 minuti, ma il contratto con  Adobe determina i valori effettivi.

I messaggi contengono le informazioni seguenti:

* Tipo di contenuto (live, lineare o VOD)
* URL contenuto
* Se gli annunci pubblicitari sono abilitati
* Se gli annunci mid-roll sono abilitati (solo VOD)
* Se il flusso è protetto da DRM
* La versione e la piattaforma TVSDK del browser

 Adobe preconfigura questa disposizione, ma se desiderate modificare la disposizione, collaborate con il rappresentante di abilitazione  Adobe.

Per monitorare le statistiche inviate al Adobe da Browser TVSDK, ottenere l&#39;URL dal rappresentante di abilitazione  Adobe e utilizzare uno strumento di acquisizione di rete, ad esempio Charles, per visualizzare i dati.
