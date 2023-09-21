---
description: Puoi tenere traccia dell’utilizzo dei video integrando Browser TVSDK con Adobe Analytics.
title: Analisi dei video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Analisi dei video{#video-analytics}

Puoi tenere traccia dell’utilizzo dei video integrando Browser TVSDK con Adobe Analytics.

Il tracciamento video nel browser TVSDK utilizza **Adobe Analytics Video Essentials** servizio, che fornisce metriche di coinvolgimento video, come visualizzazioni video, completamenti video, impressioni di annunci, tempo trascorso su video e così via. Per ulteriori informazioni su questo servizio, contatta il rappresentante del tuo Adobe.

La procedura seguente riepiloga i passaggi per attivare il tracciamento video nel lettore:

1. Inizializza e/o configura i seguenti componenti di tracciamento video:

   * **Libreria AppMeasurement** : contiene la logica di base per la raccolta dati di basso livello. Qui vengono accumulati i dati heartbeat video e inviati tramite la rete.
   * **Libreria heartbeat video** : contiene la logica di base per la raccolta dati video-heartbeat. La libreria heartbeat video accede a un sottoinsieme delle API della libreria AppMeasurement.

     >[!TIP]
     >
     >L&#39;app non interagisce direttamente con il codice heartbeat video. Al contrario, l’app utilizza le API TVSDK del browser per configurare le funzionalità di tracciamento video del lettore.

   * **Libreria VisitorID** : identifica in modo univoco i visitatori della pagina web che ospita il lettore video.

   >[!IMPORTANT]
   >
   >La funzionalità di tracciamento video integrato TVSDK nel browser dipende da un’istanza AppMeasurement configurata correttamente. Gli elementi di tracciamento presuppongono che la libreria AppMeasurement sia già stata creata un’istanza e configurata prima di configurare e attivare il tracciamento video. Le funzionalità di tracciamento video di TVSDK per browser dipendono dall’esistenza di un’istanza completamente funzionale e configurata correttamente della libreria AppMeasurement.

1. Imposta la generazione di rapporti di analisi video sul lato server utilizzando gli Strumenti di amministrazione di Adobe Analytics.
