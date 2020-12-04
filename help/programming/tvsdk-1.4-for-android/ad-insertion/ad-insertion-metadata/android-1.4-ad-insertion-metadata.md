---
description: Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come  Adobe Primetime e le decisioni, richiedono valori di configurazione per abilitare la connessione al provider.
seo-description: Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come  Adobe Primetime e le decisioni, richiedono valori di configurazione per abilitare la connessione al provider.
seo-title: Aggiungi metadati di inserimento
title: Aggiungi metadati di inserimento
uuid: f40ed53b-eba1-4f70-a29c-90cac51e8a9a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Panoramica {#ad-insertion-metadata}

Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come  Adobe Primetime e le decisioni, richiedono valori di configurazione per abilitare la connessione al provider.

TVSDK include la libreria Primetime e decisionali. Affinché il contenuto includa la pubblicità dal server di decisione degli annunci Primetime, l&#39;applicazione deve fornire le seguenti `AuditudeSettings` informazioni necessarie:

* `mediaID`, che è un identificatore univoco per il video da riprodurre.

   L&#39;editore assegna il `mediaID` durante l&#39;invio di contenuti video e informazioni pubblicitarie al server Adobe Primetime  e decisionale. Questo ID viene utilizzato da Primetime ad Decioning per recuperare informazioni pubblicitarie correlate al video dal server.

* (Facoltativo) `defaultMediaId`, che specifica gli annunci che vengono serviti quando vengono soddisfatte le seguenti condizioni:

   * La richiesta al server di annunci non è valida o il contenuto non è configurato correttamente.
   * Primetime e le decisioni relative agli annunci stanno registrando dei ritardi nella propagazione dei dati.
   * Uno dei processi back-end di Primetime e di decisione degli annunci non funziona correttamente o non è disponibile.

   >[!TIP]
   >
   > Adobe consiglia di utilizzare `defaultMediaId`.

* Il `zoneID`, assegnato dal Adobe , identifica la società o il sito Web.
* Il dominio del server di annunci assegnato.
* Altri parametri di targeting.

   Puoi includere questi parametri in base alle tue esigenze e alle esigenze del provider di annunci.