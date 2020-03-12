---
description: Potete tenere traccia dell’utilizzo dei video integrando TVSDK con Adobe Analytics.
seo-description: Potete tenere traccia dell’utilizzo dei video integrando TVSDK con Adobe Analytics.
seo-title: Integrazione di TVSDK con Adobe Analytics
title: Integrazione di TVSDK con Adobe Analytics
uuid: 4d498d35-ec8e-40fc-8272-1637ef942bb0
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Integrazione di TVSDK con Adobe Analytics {#integrating-tvsdk-with-adobe-analytics}

Potete tenere traccia dell’utilizzo dei video integrando TVSDK con Adobe Analytics.

Il tracciamento dei video in TVSDK utilizza il servizio **Adobe Analytics Video Essentials** , che fornisce metriche di coinvolgimento dei video, come visualizzazioni video, completamenti di video, impressioni di annunci, tempo trascorso sul video e così via. Per ulteriori informazioni su questo servizio, contattate il vostro rappresentante Adobe.

La procedura seguente riassume i passaggi per attivare il tracciamento video nel lettore:

1. Inizializzate e/o configurate i seguenti componenti di tracciamento video:

   >[!TIP]
   >
   >In Android, questi componenti fanno parte di TVSDK.

   * File di configurazione JSON
   * Oggetto metadati analisi video
   * Oggetto metadati globale

1. Configurate i report di analisi video sul lato server utilizzando Adobe Analytics Admin Tools.