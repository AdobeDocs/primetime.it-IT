---
description: Puoi tenere traccia dell’utilizzo dei video integrando TVSDK con Adobe Analytics.
title: Analisi dei video
exl-id: 02303511-2713-4974-ada7-6f50fc500325
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# Analisi dei video{#video-analytics}

Puoi tenere traccia dell’utilizzo dei video integrando TVSDK con Adobe Analytics.

Il tracciamento video in TVSDK utilizza **Adobe Analytics Video Essentials** servizio, che fornisce metriche di coinvolgimento video, come visualizzazioni video, completamenti video, impressioni di annunci, tempo trascorso su video e così via. Per ulteriori informazioni su questo servizio, contatta il rappresentante del tuo Adobe.

La procedura seguente riepiloga i passaggi per attivare il tracciamento video nel lettore:

1. Inizializza e/o configura i seguenti componenti di tracciamento video:

   * **Libreria AppMeasurement** : contiene la logica di base per la raccolta dati di basso livello. Qui vengono accumulati i dati heartbeat video e inviati tramite la rete.
   * **Libreria heartbeat video** : contiene la logica di base per la raccolta dati video-heartbeat. La libreria heartbeat video accede a un sottoinsieme del `AppMeasurement` API della libreria.

      >[!TIP]
      >
      >L&#39;app non interagisce direttamente con il codice heartbeat video. Al contrario, l’app utilizza le API TVSDK per configurare le funzionalità di tracciamento video del lettore.

   * **Libreria VisitorID** : identifica in modo univoco i visitatori della pagina web che ospita il lettore video.
   >[!IMPORTANT]
   >
   >La funzionalità di tracciamento video integrata di TVSDK dipende da una `AppMeasurement` dell&#39;istanza. Gli elementi di tracciamento presuppongono che `AppMeasurement` la libreria è già stata creata e configurata prima di configurare e attivare il tracciamento video. Le funzionalità di tracciamento video TVSDK dipendono dall’esistenza di un’istanza completamente funzionale e configurata correttamente del `AppMeasurement` libreria.

1. Imposta la generazione di rapporti di analisi video sul lato server utilizzando gli Strumenti di amministrazione di Adobe Analytics.
