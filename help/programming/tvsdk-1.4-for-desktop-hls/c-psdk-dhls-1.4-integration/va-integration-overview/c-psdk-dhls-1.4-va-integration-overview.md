---
description: Potete tenere traccia dell’utilizzo dei video integrando TVSDK con  Adobe Analytics.
seo-description: Potete tenere traccia dell’utilizzo dei video integrando TVSDK con  Adobe Analytics.
seo-title: Analisi video
title: Analisi video
uuid: c3cb0574-1117-409c-8aa7-641363d8d85f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Video analytics{#video-analytics}

Potete tenere traccia dell’utilizzo dei video integrando TVSDK con  Adobe Analytics.

Il tracciamento video in TVSDK utilizza il servizio **Adobe Analytics Video Essentials**, che fornisce metriche di coinvolgimento video, come visualizzazioni video, completamenti video, impressioni sugli annunci, tempo trascorso sul video e così via. Per ulteriori informazioni su questo servizio, contattate il rappresentante  Adobe.

La procedura seguente riassume i passaggi per attivare il tracciamento video nel lettore:

1. Inizializzate e/o configurate i seguenti componenti di tracciamento video:

   * **Libreria**  AppMeasurement - Contiene la logica di base della raccolta dati di basso livello. Qui i dati heartbeat video vengono accumulati e inviati attraverso la rete.
   * **Video Heartbeat library** - Contiene la logica di base della raccolta di dati heartbeat video. La libreria heartbeat video accede a un sottoinsieme delle API della libreria `AppMeasurement`.

      >[!TIP]
      >
      >L&#39;app non interagisce direttamente con il codice heartbeat video. Al contrario, l&#39;app utilizza le API TVSDK per configurare le funzionalità di tracciamento video del lettore.

   * **Libreria**  VisitorID: identifica in modo univoco i visitatori della pagina Web che ospita il lettore video.
   >[!IMPORTANT]
   >
   >La funzionalità di tracciamento video integrata TVSDK dipende da un&#39;istanza `AppMeasurement` configurata correttamente. Gli elementi di tracciamento presuppongono che la libreria `AppMeasurement` sia già stata creata e configurata prima di configurare e attivare il tracciamento video. Le funzionalità di tracciamento video TVSDK dipendono dall&#39;esistenza di un&#39;istanza della libreria `AppMeasurement` completamente funzionale e configurata correttamente.

1. Configurate i rapporti di analisi video sul lato server utilizzando  Adobe Analytics Admin Tools.

