---
description: Per soddisfare i clienti che desiderano pagare solo per ciò che utilizzano, anziché una tariffa fissa indipendentemente dall’uso effettivo, Adobe raccoglie le metriche di utilizzo e le utilizza per determinare quanto fatturare ai clienti.
title: Metriche di fatturazione
exl-id: 85974d51-3e29-42f6-bf31-1fa9ccbdd528
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Panoramica {#billing-metrics-overview}

Per soddisfare i clienti che desiderano pagare solo per ciò che utilizzano, anziché una tariffa fissa indipendentemente dall’uso effettivo, Adobe raccoglie le metriche di utilizzo e le utilizza per determinare quanto fatturare ai clienti.

Ogni volta che il lettore genera un evento di avvio del flusso, TVSDK inizia a inviare periodicamente messaggi HTTP al sistema di fatturazione di Adobe. Il periodo, noto come durata fatturabile, può essere diverso per VOD standard, pro VOD (annunci mid-roll abilitati) e contenuti live. La durata predefinita per ogni tipo di contenuto è di 30 minuti, ma il contratto con Adobe determina i valori effettivi.

I messaggi contengono le seguenti informazioni:

* Tipo di contenuto (live, lineare o VOD)
* URL contenuto
* Se gli annunci sono abilitati
* Se gli annunci mid-roll sono abilitati (solo VOD)
* Se il flusso è protetto da DRM
* Versione e piattaforma TVSDK

Adobe preconfigura questa disposizione, ma puoi lavorare con il tuo rappresentante di Adobe Enablement per modificare la disposizione, e lavorare con il tuo rappresentante di Adobe Enablement.

Per monitorare le statistiche inviate da TVSDK ad Adobe, ottieni l’URL dal tuo rappresentante per l’abilitazione dell’Adobe e utilizza uno strumento di acquisizione di rete, come Charles, per visualizzare i dati.
