---
description: Per soddisfare i clienti che desiderano pagare solo ciò che utilizzano, anziché un tasso fisso indipendentemente dall’uso effettivo, Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto fatturare ai clienti.
title: Metriche di fatturazione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---


# Panoramica {#billing-metrics-overview}

Per soddisfare i clienti che desiderano pagare solo ciò che utilizzano, anziché un tasso fisso indipendentemente dall’uso effettivo, Adobe raccoglie le metriche di utilizzo e utilizza queste metriche per determinare quanto fatturare ai clienti.

Ogni volta che il lettore genera un evento di avvio del flusso, il browser TVSDK inizia a inviare periodicamente messaggi HTTP al sistema di fatturazione di Adobe. Il periodo, noto come durata fatturabile, può essere diverso per VOD standard, pro VOD (annunci mid-roll abilitati) e contenuti live. La durata predefinita di ciascun tipo di contenuto è di 30 minuti, ma il contratto con Adobe determina i valori effettivi.

I messaggi contengono le seguenti informazioni:

* Tipo di contenuto (live, lineare o VOD)
* URL contenuto
* Se gli annunci sono abilitati
* Se gli annunci mid-roll sono abilitati (solo VOD)
* Se il flusso è protetto da DRM
* Versione e piattaforma TVSDK del browser

L&#39;Adobe preconfigura questa disposizione, ma se desideri modificarla, rivolgiti al tuo rappresentante di abilitazione Adobe.

Per monitorare le statistiche inviate ad Adobe da Browser TVSDK, ottieni l’URL dal tuo rappresentante di abilitazione Adobe e utilizza uno strumento di acquisizione di rete, ad esempio Charles, per vedere i dati.
