---
description: Potete tenere traccia dell’utilizzo dei video integrando TVSDK con  Adobe Analytics.
seo-description: Potete tenere traccia dell’utilizzo dei video integrando TVSDK con  Adobe Analytics.
seo-title: Integrazione dell'analisi video
title: Integrazione dell'analisi video
uuid: 275d2c88-a15c-4645-9234-f29d32fc4a63
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Integrazione dell&#39;analisi video {#video-analytics-integration}

Potete tenere traccia dell’utilizzo dei video integrando TVSDK con  Adobe Analytics.

Il tracciamento video in TVSDK utilizza il servizio **Adobe Analytics Video Essentials**, che fornisce metriche di coinvolgimento video, come visualizzazioni video, completamenti video, impressioni sugli annunci, tempo trascorso sul video e così via. Per ulteriori informazioni su questo servizio, contattate il rappresentante  Adobe.

La procedura seguente riassume i passaggi per attivare il tracciamento video nel lettore:

1. Inizializzate e/o configurate i seguenti componenti di tracciamento video:

   Su iOS, questi componenti fanno parte di TVSDK:

   * File di configurazione JSON
   * Oggetto metadati analisi video
   * Oggetto metadati globale
   * Oggetto tracciatore analisi video

1. Configurate i rapporti di analisi video sul lato server utilizzando  Adobe Analytics Admin Tools.