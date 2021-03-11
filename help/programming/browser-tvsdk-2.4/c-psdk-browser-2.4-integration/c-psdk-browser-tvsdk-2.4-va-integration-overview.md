---
description: È possibile tenere traccia dell’utilizzo dei video integrando l’SDK per browser con Adobe Analytics.
title: Analisi video
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Analisi video{#video-analytics}

È possibile tenere traccia dell’utilizzo dei video integrando l’SDK per browser con Adobe Analytics.

Il tracciamento video nel browser TVSDK utilizza il servizio **Adobe Analytics Video Essentials**, che fornisce metriche di coinvolgimento video, come visualizzazioni video, visualizzazioni complete di video, impressioni di annunci, tempo trascorso sul video e così via. Per ulteriori informazioni su questo servizio, contatta il tuo rappresentante di Adobe.

La procedura seguente riassume i passaggi per attivare il tracciamento video nel lettore:

1. Inizializzare e/o configurare i seguenti componenti di tracciamento video:

   * **Libreria AppMeasurement**  - Contiene la logica di base della raccolta dati di basso livello. Qui i dati dell&#39;heartbeat video vengono accumulati e inviati attraverso la rete.
   * **Libreria heartbeat video**  - Contiene la logica di base della raccolta dati video-heartbeat. La libreria heartbeat video accede a un sottoinsieme delle API della libreria AppMeasurement.

      >[!TIP]
      >
      >L&#39;app non interagisce direttamente con il codice heartbeat video. Al contrario, l’app utilizza le API TVSDK per browser per configurare le funzionalità di tracciamento video del lettore.

   * **Libreria VisitorID** : identifica in modo univoco i visitatori della pagina web che ospita il lettore video.
   >[!IMPORTANT]
   >
   >La funzionalità di tracciamento video integrato del browser TVSDK dipende da un&#39;istanza AppMeasurement configurata correttamente. Gli elementi di tracciamento presuppongono che la libreria AppMeasurement sia già creata e configurata prima di configurare e attivare il tracciamento video. Le funzionalità di tracciamento video TVSDK per browser dipendono dall’esistenza di un’istanza completamente funzionale e configurata correttamente della libreria AppMeasurement.

1. Imposta i rapporti di analisi video sul lato server utilizzando gli strumenti di amministrazione di Adobe Analytics.