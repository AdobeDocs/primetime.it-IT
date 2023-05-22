---
description: Puoi tenere traccia dell’utilizzo dei video integrando TVSDK con Adobe Analytics.
title: Integrazione di TVSDK con Adobe Analytics
exl-id: d6e235ad-dffb-4503-bf6f-f7a780523791
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Integrazione di TVSDK con Adobe Analytics {#integrating-tvsdk-with-adobe-analytics}

Puoi tenere traccia dell’utilizzo dei video integrando TVSDK con Adobe Analytics.

Il tracciamento video in TVSDK utilizza **Adobe Analytics Video Essentials** servizio, che fornisce metriche di coinvolgimento video, come visualizzazioni video, completamenti video, impressioni di annunci, tempo trascorso su video e così via. Per ulteriori informazioni su questo servizio, contatta il rappresentante del tuo Adobe.

La procedura seguente riepiloga i passaggi per attivare il tracciamento video nel lettore:

1. Inizializza e/o configura i seguenti componenti di tracciamento video:

   >[!TIP]
   >
   >In Android, questi componenti fanno parte di TVSDK.

   * File di configurazione JSON
   * Oggetto metadati di analisi video
   * Oggetto metadati globale

1. Imposta la generazione di rapporti di analisi video sul lato server utilizzando gli Strumenti di amministrazione di Adobe Analytics.
