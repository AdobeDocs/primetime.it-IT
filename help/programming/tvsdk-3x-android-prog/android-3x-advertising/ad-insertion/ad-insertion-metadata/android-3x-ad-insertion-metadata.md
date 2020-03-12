---
description: Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come Adobe Primetime ad Decioning, richiedono valori di configurazione per abilitare la connessione al provider.
seo-description: Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come Adobe Primetime ad Decioning, richiedono valori di configurazione per abilitare la connessione al provider.
seo-title: Aggiungi metadati di inserimento
title: Aggiungi metadati di inserimento
uuid: 676e81b9-4c2b-487e-bc68-74879ca2966b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Panoramica {#ad-nsertion-metadata-overview}

Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come Adobe Primetime ad Decioning, richiedono valori di configurazione per abilitare la connessione al provider.

TVSDK include la libreria Primetime e Decioninglary. Affinché il contenuto includa la pubblicità proveniente dal server di decisione degli annunci Primetime, l&#39;applicazione deve fornire le `AuditudeSettings` informazioni necessarie seguenti:

* `mediaID`, che è un identificatore univoco per il video da riprodurre.

   L&#39;editore assegna il mediaID quando invia contenuti video e informazioni sull&#39;annuncio al server Adobe Primetime ad Ad Decision. Questo ID viene utilizzato da Primetime ad Decisioningper recuperare dal server le informazioni pubblicitarie correlate al video.

* (Facoltativo) `defaultMediaId`, che specifica gli annunci che vengono serviti quando vengono soddisfatte le seguenti condizioni:

   * La richiesta al server di annunci non è valida o il contenuto non è configurato correttamente.
   * Primetime e decisione sull&#39;annuncio stanno riscontrando dei ritardi nella propagazione dei dati.
   * Uno dei processi back-end di Primetime e di decisione degli annunci non funziona correttamente o non è disponibile.
   >[!TIP]
   >
   >Adobe consiglia di utilizzare `defaultMediaId`.

* Il vostro `zoneID`, assegnato da Adobe, identifica la vostra società o il vostro sito Web.
* Il dominio del server di annunci assegnato.
* Altri parametri di targeting.

   Puoi includere questi parametri in base alle tue esigenze e alle esigenze del provider di annunci.