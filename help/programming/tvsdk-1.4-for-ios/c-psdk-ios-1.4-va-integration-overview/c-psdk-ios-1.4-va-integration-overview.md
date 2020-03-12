---
description: Potete tenere traccia dell’utilizzo dei video integrando TVSDK con Adobe Analytics.
seo-description: Potete tenere traccia dell’utilizzo dei video integrando TVSDK con Adobe Analytics.
seo-title: Analisi video
title: Analisi video
uuid: 8f297316-f95e-4896-b489-a2d6b36e6b40
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Integrazione dell&#39;analisi video {#video-analytics-integration}

Potete tenere traccia dell’utilizzo dei video integrando TVSDK con Adobe Analytics.

Il tracciamento dei video in TVSDK utilizza il servizio **Adobe Analytics Video Essentials** , che fornisce metriche di coinvolgimento dei video, come visualizzazioni video, completamenti di video, impressioni di annunci, tempo trascorso sul video e così via. Per ulteriori informazioni su questo servizio, contattate il vostro rappresentante Adobe.

La procedura seguente riassume i passaggi per attivare il tracciamento video nel lettore:

1. Inizializzate e/o configurate i seguenti componenti di tracciamento video:

   Su iOS, questi componenti fanno parte di TVSDK:

   * File di configurazione JSON
   * Oggetto metadati analisi video
   * Oggetto metadati globale
   * Oggetto tracciatore analisi video

1. Configurate i report di analisi video sul lato server utilizzando Adobe Analytics Admin Tools.