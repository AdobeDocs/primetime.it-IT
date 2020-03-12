---
description: TVSDK contatta un servizio di distribuzione di annunci, come Adobe Primetime ad Decioning, e tenta di ottenere il file playlist principale che corrisponde al flusso video per l'annuncio. Durante la fase di risoluzione degli annunci, TVSDK effettua una chiamata HTTP al server remoto di distribuzione degli annunci e analizza la risposta del server.
seo-description: TVSDK contatta un servizio di distribuzione di annunci, come Adobe Primetime ad Decioning, e tenta di ottenere il file playlist principale che corrisponde al flusso video per l'annuncio. Durante la fase di risoluzione degli annunci, TVSDK effettua una chiamata HTTP al server remoto di distribuzione degli annunci e analizza la risposta del server.
seo-title: Fase di risoluzione degli annunci
title: Fase di risoluzione degli annunci
uuid: b3e62a57-7e62-4e4e-8fa6-0d416785db67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Fase di risoluzione degli annunci{#ad-resolving-phase}

TVSDK contatta un servizio di distribuzione di annunci, come Adobe Primetime ad Decioning, e tenta di ottenere il file playlist principale che corrisponde al flusso video per l&#39;annuncio. Durante la fase di risoluzione degli annunci, TVSDK effettua una chiamata HTTP al server remoto di distribuzione degli annunci e analizza la risposta del server.

TVSDK supporta i seguenti tipi di provider di annunci:

* Metadati e provider

   I dati dell&#39;annuncio vengono codificati in file JSON in testo normale.
* Primetime e fornitore di annunci pubblicitari con decisione

   TVSDK invia una richiesta, inclusa una serie di parametri di targeting e un numero di identificazione della risorsa, al server back-end di Primetime e di decisione. Primetime e il processo decisionale degli annunci risponde con un documento SMIL (lingua di integrazione multimediale sincronizzata) che contiene le informazioni sugli annunci richieste.
* Fornitore di indicatori di annunci personalizzati

   Gestisce la situazione in cui gli annunci vengono masterizzati nel flusso, dal lato server. TVSDK non esegue l&#39;inserimento effettivo degli annunci, ma deve tenere traccia degli annunci inseriti sul lato server. Questo provider imposta i marcatori di annunci utilizzati da TVSDK per eseguire il tracciamento degli annunci.

Durante questa fase può verificarsi una delle seguenti situazioni di failover:

* Non è possibile recuperare i dati per motivi che includono una mancanza di connettività o un errore lato server, ad esempio una risorsa non trovata e così via.
* I dati sono stati recuperati, ma il formato non è valido.

   Ciò potrebbe verificarsi perché, ad esempio, l&#39;analisi dei dati in entrata non è riuscita.

TVSDK invia una notifica di avviso relativa all&#39;errore e continua l&#39;elaborazione.
