---
description: Per consentire il funzionamento del risolutore di annunci, i fornitori di annunci, come Adobe Primetime ad decision, richiedono valori di configurazione per abilitare la connessione al provider.
title: Metadati di inserimento annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Panoramica {#ad-insertion-metadata}

Per consentire il funzionamento del risolutore di annunci, i fornitori di annunci, come Adobe Primetime ad decision, richiedono valori di configurazione per abilitare la connessione al provider.

TVSDK include la libreria Primetime ad decision ioning. Affinché i contenuti includano la pubblicità dal server di ad decisioning di Primetime, l&#39;applicazione deve fornire le seguenti informazioni `AuditudeSettings` necessarie:

* `mediaID`, che è un identificatore univoco per il video da riprodurre.

   L’editore assegna il `mediaID` quando invia contenuti video e informazioni sugli annunci al server Adobe Primetime ad decision ioning. Questo ID viene utilizzato da Primetime ad decision per recuperare dal server le informazioni pubblicitarie correlate al video.

* (Facoltativo) `defaultMediaId`, che specifica gli annunci che vengono serviti quando vengono soddisfatte le seguenti condizioni:

   * La richiesta al server di annunci non è valida o il contenuto non è configurato correttamente.
   * Primetime ad Decioning sta riscontrando ritardi nella propagazione dei dati.
   * Uno dei processi back-end di Primetime ad Decioning non funziona correttamente o non è disponibile.

   >[!TIP]
   >
   >Adobe consiglia di utilizzare `defaultMediaId`.

* Il `zoneID`, assegnato per Adobe, identifica l&#39;azienda o il sito web.
* Dominio del server di annunci assegnato.
* Altri parametri di targeting.

   Puoi includere questi parametri in base alle tue esigenze e alle esigenze del provider di annunci.