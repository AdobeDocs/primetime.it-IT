---
description: Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come  Adobe Primetime e le decisioni, richiedono valori di configurazione per abilitare la connessione al provider.
seo-description: Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come  Adobe Primetime e le decisioni, richiedono valori di configurazione per abilitare la connessione al provider.
seo-title: Aggiungi metadati di inserimento
title: Aggiungi metadati di inserimento
uuid: ee4dd8b8-4c41-4f01-be50-60f4c7dc962d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---


# Panoramica {#ad-insertion-metadata-overview}

Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come  Adobe Primetime e le decisioni, richiedono valori di configurazione per abilitare la connessione al provider.

TVSDK include la libreria Primetime e Decioninglary. Affinché il contenuto includa la pubblicità dal server di decisione annunci Primetime, l&#39;applicazione deve fornire le seguenti informazioni `AuditudeSettings` richieste:

* `mediaID`, che è un identificatore univoco per il video da riprodurre.

   L’editore assegna il mediaID quando invia contenuti video e informazioni sull’annuncio al server Adobe Primetime  e decisionale. Questo ID viene utilizzato da Primetime ad Decisioningper recuperare dal server le informazioni pubblicitarie correlate al video.

* (Facoltativo) `defaultMediaId`, che specifica gli annunci che vengono serviti quando vengono soddisfatte le seguenti condizioni:

   * La richiesta al server di annunci non è valida o il contenuto non è configurato correttamente.
   * Primetime ad Decisioningè in ritardo nella propagazione dei dati.
   * Uno dei processi back-end di Primetime e di decisione degli annunci non funziona correttamente o non è disponibile.

   >[!TIP]
   >
   > Adobe consiglia di utilizzare `defaultMediaId`.

* Il `zoneID`, assegnato dal Adobe , identifica la società o il sito Web.
* Il dominio del server di annunci assegnato.
* Altri parametri di targeting.

   Puoi includere questi parametri in base alle tue esigenze e alle esigenze del provider di annunci.