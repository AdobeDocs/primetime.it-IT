---
description: Per soddisfare i clienti che desiderano pagare solo per ciò che utilizzano, anziché una tariffa fissa indipendentemente dall’uso effettivo, Adobe raccoglie le metriche di utilizzo e le utilizza per determinare quanto fatturare ai clienti.
title: Metriche di fatturazione
exl-id: f4200573-571f-4ed3-be8c-08b72d4f9e0e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Panoramica {#billing-metrics-overview}

Per soddisfare i clienti che desiderano pagare solo per ciò che utilizzano, anziché una tariffa fissa indipendentemente dall’uso effettivo, Adobe raccoglie le metriche di utilizzo e le utilizza per determinare quanto fatturare ai clienti.

Ogni volta che il lettore genera un evento di avvio del flusso, il TVSDK del browser inizia a inviare periodicamente messaggi HTTP al sistema di fatturazione di Adobe. Il periodo, noto come durata fatturabile, può essere diverso per VOD standard, pro VOD (annunci mid-roll abilitati) e contenuti live. La durata predefinita per ogni tipo di contenuto è di 30 minuti, ma il contratto con Adobe determina i valori effettivi.

I messaggi contengono le seguenti informazioni:

* Tipo di contenuto (live, lineare o VOD)
* URL contenuto
* Se gli annunci sono abilitati
* Se gli annunci mid-roll sono abilitati (solo VOD)
* Se il flusso è protetto da DRM
* Versione e piattaforma TVSDK del browser

Adobe preconfigura questa disposizione, ma se desideri modificarla, rivolgiti al tuo rappresentante Adobe Enablement.

Per monitorare le statistiche inviate da Browser TVSDK all’Adobe, ottieni l’URL dal tuo rappresentante per l’abilitazione dell’Adobe e utilizza uno strumento di acquisizione di rete, ad esempio Charles, per visualizzare i dati.
