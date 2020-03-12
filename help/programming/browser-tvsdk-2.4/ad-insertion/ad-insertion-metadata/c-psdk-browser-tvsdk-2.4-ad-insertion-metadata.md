---
description: Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come Adobe Primetime ad Decioning, richiedono valori di configurazione per abilitare la connessione al provider.
seo-description: Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come Adobe Primetime ad Decioning, richiedono valori di configurazione per abilitare la connessione al provider.
seo-title: Aggiungi metadati di inserimento
title: Aggiungi metadati di inserimento
uuid: 8848c939-1f12-4145-8025-453b4fe79aae
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Panoramica {#ad-insertion-metadata-overview}

Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come Adobe Primetime ad Decioning, richiedono valori di configurazione per abilitare la connessione al provider.

Il browser TVSDK include la libreria Adobe Primetime e decisionali. Affinché il contenuto includa la pubblicità proveniente dal server Adobe Primetime e decisionali, l&#39;applicazione deve fornire le seguenti informazioni sulle impostazioni audio richieste:

* `mediaID`, che è un identificatore univoco per il video da riprodurre.

   L&#39;editore assegna il mediaID quando invia contenuti video e informazioni sull&#39;annuncio al server Adobe Primetime ad Ad Decision. Questo ID viene utilizzato da Adobe Primetime ad esempio per ottenere dal server informazioni pubblicitarie correlate al video.

* (Facoltativo) `defaultMediaId`, che specifica gli annunci che vengono serviti quando vengono soddisfatte le seguenti condizioni:

   * La richiesta al server di annunci non è valida o il contenuto non è configurato correttamente.
   * Le decisioni relative agli annunci Adobe Primetime registrano dei ritardi nella propagazione dei dati.
   * Uno dei processi back-end di Adobe Primetime e di decisione degli annunci non funziona correttamente o non è disponibile.
   >[!TIP]
   >
   >Adobe consiglia di utilizzare `defaultMediaId`.

* Il vostro `zoneID`, assegnato da Adobe, identifica la vostra società o il vostro sito Web.
* Il dominio del server di annunci assegnato.
* Altri parametri di targeting.

   Puoi includere questi parametri in base alle tue esigenze e alle esigenze del provider di annunci.