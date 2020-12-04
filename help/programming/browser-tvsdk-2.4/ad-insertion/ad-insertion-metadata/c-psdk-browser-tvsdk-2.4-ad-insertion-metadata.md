---
description: Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come  Adobe Primetime e le decisioni, richiedono valori di configurazione per abilitare la connessione al provider.
seo-description: Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come  Adobe Primetime e le decisioni, richiedono valori di configurazione per abilitare la connessione al provider.
seo-title: Aggiungi metadati di inserimento
title: Aggiungi metadati di inserimento
uuid: 8848c939-1f12-4145-8025-453b4fe79aae
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Panoramica {#ad-insertion-metadata-overview}

Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come  Adobe Primetime e le decisioni, richiedono valori di configurazione per abilitare la connessione al provider.

Browser TVSDK include la libreria  Adobe Primetime e decisionale. Affinché il contenuto includa la pubblicità proveniente dal server  Adobe Primetime e decisionale, l&#39;applicazione deve fornire le seguenti informazioni sulle impostazioni audio richieste:

* `mediaID`, che è un identificatore univoco per il video da riprodurre.

   L’editore assegna il mediaID quando invia contenuti video e informazioni sull’annuncio al server Adobe Primetime  e decisionale. Questo ID viene utilizzato da  ad Decioning Adobe Primetime per recuperare informazioni pubblicitarie correlate al video dal server.

* (Facoltativo) `defaultMediaId`, che specifica gli annunci che vengono serviti quando vengono soddisfatte le seguenti condizioni:

   * La richiesta al server di annunci non è valida o il contenuto non è configurato correttamente.
   *  Adobe Primetime sta registrando dei ritardi nella propagazione dei dati.
   * Uno dei  processi back-end di Adobe Primetime e di decisione degli annunci pubblicitari è malfunzionante o non disponibile.

   >[!TIP]
   >
   > Adobe consiglia di utilizzare `defaultMediaId`.

* Il `zoneID`, assegnato dal Adobe , identifica la società o il sito Web.
* Il dominio del server di annunci assegnato.
* Altri parametri di targeting.

   Puoi includere questi parametri in base alle tue esigenze e alle esigenze del provider di annunci.