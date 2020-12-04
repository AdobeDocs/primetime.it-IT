---
description: Potete tenere traccia dell’utilizzo dei video integrando Browser TVSDK con  Adobe Analytics.
seo-description: Potete tenere traccia dell’utilizzo dei video integrando Browser TVSDK con  Adobe Analytics.
seo-title: Analisi video
title: Analisi video
uuid: 6351933b-c0f3-4e3e-ad27-bedc8eecc312
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Video analytics{#video-analytics}

Potete tenere traccia dell’utilizzo dei video integrando Browser TVSDK con  Adobe Analytics.

Il tracciamento dei video nel browser TVSDK utilizza il servizio **Adobe Analytics Video Essentials**, che fornisce metriche di coinvolgimento dei video, come visualizzazioni video, completamenti dei video, impressioni degli annunci, tempo trascorso sul video e così via. Per ulteriori informazioni su questo servizio, contattate il rappresentante  Adobe.

La procedura seguente riassume i passaggi per attivare il tracciamento video nel lettore:

1. Inizializzate e/o configurate i seguenti componenti di tracciamento video:

   * **Libreria**  AppMeasurement - Contiene la logica di base della raccolta dati di basso livello. Qui i dati heartbeat video vengono accumulati e inviati attraverso la rete.
   * **Video Heartbeat library** - Contiene la logica di base della raccolta di dati heartbeat video. La libreria heartbeat video accede a un sottoinsieme delle API della libreria AppMeasurement.

      >[!TIP]
      >
      >L&#39;app non interagisce direttamente con il codice heartbeat video. Al contrario, l&#39;app utilizza le API TVSDK del browser per configurare le funzionalità di tracciamento video del lettore.

   * **Libreria**  VisitorID: identifica in modo univoco i visitatori della pagina Web che ospita il lettore video.
   >[!IMPORTANT]
   >
   >La funzionalità di tracciamento video integrata nel browser TVSDK dipende da un&#39;istanza AppMeasurement configurata correttamente. Gli elementi di tracciamento presuppongono che la libreria AppMeasurement sia già stata creata e configurata prima di configurare e attivare il tracciamento video. Le funzionalità di tracciamento video TVSDK per browser dipendono dall&#39;esistenza di un&#39;istanza completamente funzionale e configurata correttamente della libreria AppMeasurement.

1. Configurate i rapporti di analisi video sul lato server utilizzando  Adobe Analytics Admin Tools.