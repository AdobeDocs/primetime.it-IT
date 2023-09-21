---
description: TVSDK contatta un servizio di consegna degli annunci, come Adobe Primetime ad decisioning, e tenta di ottenere il file della playlist principale che corrisponde al flusso video per l’annuncio. Durante la fase di risoluzione degli annunci, TVSDK effettua una chiamata HTTP al server di consegna degli annunci remoto e analizza la risposta del server.
title: Fase di risoluzione degli annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# Fase di risoluzione degli annunci{#ad-resolving-phase}

TVSDK contatta un servizio di consegna degli annunci, come Adobe Primetime ad decisioning, e tenta di ottenere il file della playlist principale che corrisponde al flusso video per l’annuncio. Durante la fase di risoluzione degli annunci, TVSDK effettua una chiamata HTTP al server di consegna degli annunci remoto e analizza la risposta del server.

TVSDK supporta i seguenti tipi di provider di annunci:

* Provider di annunci metadati

  I dati dell’annuncio sono codificati in file JSON di testo normale.
* Provider di annunci di Ad Decisioning di Primetime

  TVSDK invia una richiesta, contenente un set di parametri di targeting e un numero di identificazione della risorsa, al server back-end di Primetime ad decisioning. Primetime ad decisioning risponde con un documento SMIL (Synchronized Multimedia Integration Language) contenente le informazioni sull’annuncio richieste.
* Provider di marcatori annunci personalizzati

  Gestisce la situazione in cui gli annunci vengono masterizzati nel flusso, dal lato server. TVSDK non esegue l’inserimento effettivo dell’annuncio, ma deve tenere traccia degli annunci inseriti sul lato server. Questo provider imposta i marcatori annuncio utilizzati da TVSDK per eseguire il tracciamento degli annunci.

Durante questa fase può verificarsi una delle seguenti situazioni di failover:

* Non è possibile recuperare i dati per motivi quali mancanza di connettività o errore lato server, ad esempio l’impossibilità di trovare una risorsa e così via.
* I dati sono stati recuperati, ma il formato non è valido.

  Ciò potrebbe verificarsi, ad esempio, perché l’analisi dei dati in entrata non è riuscita.

TVSDK invia una notifica di avviso relativa all’errore e continua l’elaborazione.
