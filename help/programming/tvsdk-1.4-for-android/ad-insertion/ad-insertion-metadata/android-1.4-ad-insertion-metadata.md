---
description: Per consentire il funzionamento del resolver dell’annuncio, i provider di annunci, come Adobe Primetime ad decisioning, richiedono valori di configurazione per abilitare la connessione al provider.
title: Metadati di inserimento annuncio
exl-id: 7245b42c-f3ba-43ec-b895-c1a2d66aa11f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Panoramica {#ad-insertion-metadata}

Per consentire il funzionamento del resolver dell’annuncio, i provider di annunci, come Adobe Primetime ad decisioning, richiedono valori di configurazione per abilitare la connessione al provider.

TVSDK include la libreria Ad Decisioning di Primetime. Affinché il contenuto includa la pubblicità dal server Primetime ad decisioning, l’applicazione deve fornire i seguenti elementi obbligatori `AuditudeSettings` informazioni:

* `mediaID`, che è un identificatore univoco del video da riprodurre.

   L’editore assegna il `mediaID` durante l’invio di contenuti video e informazioni sugli annunci al server Adobe Primetime ad decisioning. Questo ID viene utilizzato da Primetime ad Decisioning per recuperare dal server le informazioni pubblicitarie correlate al video.

* (Facoltativo) `defaultMediaId`, che specifica gli annunci pubblicati quando sono soddisfatte le seguenti condizioni:

   * La richiesta al server di annunci non è valida o il contenuto non è configurato correttamente.
   * Primetime ad Decisioning sta riscontrando ritardi nella propagazione dei dati.
   * Uno dei processi back-end di Primetime ad decisioning non funziona correttamente o non è disponibile.

   >[!TIP]
   >
   >L’Adobe consiglia di utilizzare `defaultMediaId`.

* Il tuo `zoneID`, che viene assegnato da Adobe, identifica la tua azienda o il tuo sito web.
* Il dominio del server di annunci assegnato.
* Altri parametri di targeting.

   Puoi includere questi parametri in base alle tue esigenze e a quelle del provider di annunci.
