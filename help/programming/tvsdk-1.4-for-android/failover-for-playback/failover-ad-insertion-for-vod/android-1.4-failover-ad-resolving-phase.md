---
description: TVSDK contatta un servizio di consegna annunci, come Adobe Primetime ad decision, e tenta di ottenere il file playlist principale che corrisponde al flusso video per l'annuncio. Durante la fase di risoluzione degli annunci, TVSDK effettua una chiamata HTTP al server remoto di consegna degli annunci e analizza la risposta del server.
title: Fase di risoluzione degli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# Fase di risoluzione annunci{#ad-resolving-phase}

TVSDK contatta un servizio di consegna annunci, come Adobe Primetime ad decision, e tenta di ottenere il file playlist principale che corrisponde al flusso video per l&#39;annuncio. Durante la fase di risoluzione degli annunci, TVSDK effettua una chiamata HTTP al server remoto di consegna degli annunci e analizza la risposta del server.

TVSDK supporta i seguenti tipi di provider di annunci:

* Metadati e provider

   I dati dell’annuncio vengono codificati in file JSON in formato testo normale.
* Primetime ad decision provider

   TVSDK invia una richiesta, incluso un set di parametri di targeting e un numero di identificazione della risorsa, al server back-end Primetime ad Decioning. Primetime ad Decioning risponde con un documento SMIL (sincronizzato multimedia integration language) che contiene le informazioni richieste per l&#39;annuncio.
* Fornitore di indicatori di annunci personalizzati

   Gestisce la situazione in cui gli annunci vengono bruciati nel flusso, dal lato server. TVSDK non esegue l’inserimento effettivo degli annunci, ma deve tenere traccia degli annunci inseriti sul lato server. Questo provider imposta i marcatori di annunci utilizzati da TVSDK per eseguire il tracciamento degli annunci.

In questa fase può verificarsi una delle seguenti situazioni di failover:

* Impossibile recuperare i dati per motivi quali mancanza di connettività o errore lato server, ad esempio non è possibile trovare una risorsa e così via.
* I dati sono stati recuperati, ma il formato non è valido.

   Ciò potrebbe verificarsi perché, ad esempio, l’analisi dei dati in entrata non è riuscita.

TVSDK invia una notifica di avviso relativa all’errore e continua l’elaborazione.
