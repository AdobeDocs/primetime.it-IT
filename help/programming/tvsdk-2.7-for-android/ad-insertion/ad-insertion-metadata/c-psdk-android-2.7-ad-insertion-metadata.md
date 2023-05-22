---
description: Per consentire il funzionamento del resolver dell’annuncio, i provider di annunci, come Adobe Primetime ad decisioning, richiedono valori di configurazione per abilitare la connessione al provider.
title: Metadati di inserimento annuncio
exl-id: fb78da4c-129e-4ecd-b598-3ab8af40d713
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Panoramica {#ad-insertion-metadata-overview}

Per consentire il funzionamento del resolver dell’annuncio, i provider di annunci, come Adobe Primetime ad decisioning, richiedono valori di configurazione per abilitare la connessione al provider.

TVSDK include la libreria Primetime ad decisioninglibrary. Affinché il contenuto includa la pubblicità da Primetime ad decisioningserver, l’applicazione deve fornire i seguenti elementi `AuditudeSettings` informazioni:

* `mediaID`, che è un identificatore univoco del video da riprodurre.

   L’editore assegna il mediaID quando invia il contenuto video e le informazioni sugli annunci al server Adobe Primetime ad decisioning. Questo ID viene utilizzato da Primetime ad decisioningper recuperare le informazioni pubblicitarie correlate per il video dal server.

* (Facoltativo) `defaultMediaId`, che specifica gli annunci pubblicati quando sono soddisfatte le seguenti condizioni:

   * La richiesta al server di annunci non è valida o il contenuto non è configurato correttamente.
   * In Primetime ad decisioningsi verificano ritardi nella propagazione dei dati.
   * Uno dei processi back-end di Primetime ad decisioning non funziona correttamente o non è disponibile.

   >[!TIP]
   >
   >L’Adobe consiglia di utilizzare `defaultMediaId`.

* Il tuo `zoneID`, che viene assegnato da Adobe, identifica la tua azienda o il tuo sito web.
* Il dominio del server di annunci assegnato.
* Altri parametri di targeting.

   Puoi includere questi parametri in base alle tue esigenze e a quelle del provider di annunci.
