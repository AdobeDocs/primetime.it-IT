---
description: Per consentire il funzionamento del resolver dell’annuncio, i provider di annunci, come Adobe Primetime ad decisioning, richiedono valori di configurazione per abilitare la connessione al provider.
title: Metadati di inserimento annuncio
exl-id: 8d6cb371-8666-4b55-b828-0f1d495e7fb7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Panoramica {#ad-insertion-metadata-overview}

Per consentire il funzionamento del resolver dell’annuncio, i provider di annunci, come Adobe Primetime ad decisioning, richiedono valori di configurazione per abilitare la connessione al provider.

Il browser TVSDK include la libreria Adobe Primetime ad decisioning. Affinché il contenuto includa la pubblicità dal server Adobe Primetime ad decisioning, l’applicazione deve fornire le seguenti informazioni obbligatorie su AudienceSettings:

* `mediaID`, che è un identificatore univoco del video da riprodurre.

   L’editore assegna il mediaID quando invia il contenuto video e le informazioni sugli annunci al server Adobe Primetime ad decisioning. Questo ID viene utilizzato da Adobe Primetime ad Decisioning per recuperare dal server le informazioni pubblicitarie correlate al video.

* (Facoltativo) `defaultMediaId`, che specifica gli annunci pubblicati quando sono soddisfatte le seguenti condizioni:

   * La richiesta al server di annunci non è valida o il contenuto non è configurato correttamente.
   * Adobe Primetime ad Decisioning sta riscontrando ritardi nella propagazione dei dati.
   * Uno dei processi back-end di Adobe Primetime ad decisioning non funziona correttamente o non è disponibile.

   >[!TIP]
   >
   >L’Adobe consiglia di utilizzare `defaultMediaId`.

* Il tuo `zoneID`, che viene assegnato da Adobe, identifica la tua azienda o il tuo sito web.
* Il dominio del server di annunci assegnato.
* Altri parametri di targeting.

   Puoi includere questi parametri in base alle tue esigenze e a quelle del provider di annunci.
