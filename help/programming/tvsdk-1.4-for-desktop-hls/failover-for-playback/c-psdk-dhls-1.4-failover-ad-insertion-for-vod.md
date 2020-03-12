---
description: Il processo di inserimento video on-demand (VOD) consiste nelle fasi di risoluzione degli annunci, inserimento di annunci e riproduzione di annunci. Per il tracciamento degli annunci, TVSDK deve informare un server di tracciamento remoto dell'avanzamento della riproduzione di ciascun annuncio. In caso di situazioni impreviste, l'utente adotta le misure appropriate.
seo-description: Il processo di inserimento video on-demand (VOD) consiste nelle fasi di risoluzione degli annunci, inserimento di annunci e riproduzione di annunci. Per il tracciamento degli annunci, TVSDK deve informare un server di tracciamento remoto dell'avanzamento della riproduzione di ciascun annuncio. In caso di situazioni impreviste, l'utente adotta le misure appropriate.
seo-title: Inserimento pubblicitario e failover per VOD
title: Inserimento pubblicitario e failover per VOD
uuid: 98505f63-ac43-4ff5-9f7b-895b6135df47
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Inserimento pubblicitario e failover per VOD{#advertising-insertion-and-failover-for-vod}

Il processo di inserimento video on-demand (VOD) consiste nelle fasi di risoluzione degli annunci, inserimento di annunci e riproduzione di annunci. Per il tracciamento degli annunci, TVSDK deve informare un server di tracciamento remoto dell&#39;avanzamento della riproduzione di ciascun annuncio. In caso di situazioni impreviste, l&#39;utente adotta le misure appropriate.

## Fase di risoluzione degli annunci {#section_0D45C6094D724B55868B48F9A3557A8B}

TVSDK contatta un servizio di distribuzione di annunci, come Adobe Primetime ad Decioning, e tenta di ottenere il file playlist principale che corrisponde al flusso video per l&#39;annuncio. Durante la fase di risoluzione degli annunci, TVSDK effettua una chiamata HTTP al server remoto di distribuzione degli annunci e analizza la risposta del server.

TVSDK supporta i seguenti tipi di provider di annunci:

* Metadati e provider

   I dati dell&#39;annuncio vengono codificati in file JSON in testo normale.
* Primetime e fornitore di annunci pubblicitari con decisione

   TVSDK invia una richiesta, inclusa una serie di parametri di targeting e un numero di identificazione della risorsa, al server back-end di Primetime e di decisione. Primetime e il processo decisionale degli annunci risponde con un documento SMIL (lingua di integrazione multimediale sincronizzata) che contiene le informazioni sugli annunci richieste.

Durante questa fase può verificarsi una delle seguenti situazioni di failover:

* Non è possibile recuperare i dati per motivi che includono una mancanza di connettività o un errore lato server, ad esempio una risorsa non trovata e così via.
* I dati sono stati recuperati, ma il formato non è valido.

   Ciò potrebbe verificarsi perché, ad esempio, l&#39;analisi dei dati in entrata non è riuscita.

TVSDK invia una notifica di avviso relativa all&#39;errore e continua l&#39;elaborazione.

## Fase di inserimento annunci {#section_1B18E8B5768B4873B3346294175B7340}

TVSDK inserisce nella timeline il contenuto alternativo (annunci) che corrisponde al contenuto principale.

Al termine della fase di risoluzione degli annunci, TVSDK dispone di un elenco ordinato di risorse pubblicitarie raggruppate in interruzioni di annunci. Ogni interruzione di annuncio viene posizionata sulla timeline del contenuto principale utilizzando un valore di ora iniziale espresso in millisecondi (ms). Ogni annuncio in un&#39;interruzione annuncio ha una proprietà di durata che è anche espressa in ms. Gli annunci in un&#39;interruzione di pubblicità vengono concatenati uno dopo l&#39;altro. Di conseguenza, la durata di un&#39;interruzione di annuncio è uguale alla somma delle durate dei singoli annunci compositi.

Il failover può verificarsi in questa fase con conflitti che potrebbero verificarsi sulla timeline durante l&#39;inserimento di annunci. Per combinazioni specifiche di valori di inizio/durata dell&#39;interruzione di annunci, i segmenti di annunci potrebbero sovrapporsi. La sovrapposizione si verifica quando l&#39;ultima parte di un&#39;interruzione di annuncio interseca l&#39;inizio del primo annuncio nell&#39;interruzione di annuncio successiva. In queste situazioni, scarta l’interruzione annuncio successiva e continua il processo di inserimento degli annunci con la voce successiva nell’elenco fino a quando tutte le interruzioni di annuncio non vengono inserite o eliminate.

TVSDK invia una notifica di avviso relativa all&#39;errore e continua l&#39;elaborazione.

## Fase ad-riproduzione {#section_64777BD2CDA84EACB0A4EA6D68367CF5}

TVSDK scarica i segmenti di annunci e li visualizza sullo schermo del dispositivo.

A questo punto, TVSDK ha risolto gli annunci, li ha posizionati sulla timeline e tenta di eseguire il rendering del contenuto sullo schermo.

In questa fase potrebbero verificarsi le seguenti classi principali di errori:

* Errori durante la connessione al server host
* Errori durante il download del file manifesto
* Errori durante il download dei segmenti multimediali

Per tutte e tre le classi di errore, TVSDK inoltra all&#39;applicazione gli eventi attivati, inclusi:

* Eventi di notifica attivati in caso di failover.
* Eventi di notifica quando il profilo viene modificato a causa dell&#39;algoritmo di failover.
* Gli eventi di notifica attivati quando sono state prese in considerazione tutte le opzioni di failover e non è possibile eseguire automaticamente alcuna azione aggiuntiva.

   La tua applicazione deve intraprendere l&#39;azione appropriata.

Che si verifichino o meno errori, le chiamate TVSDK `AdBreakPlaybackEvent.AD_BREAK_COMPLETE` per ogni `AdBreakPlaybackEvent.AD_BREAK_STARTED` e `AdPlaybackEvent.AD_COMPLETED` per ogni `AdPLaybackEvent.AD_STARTED`. Tuttavia, se non è stato possibile scaricare i segmenti, potrebbero verificarsi degli spazi nella timeline. Quando gli spazi vuoti sono sufficientemente grandi, i valori nella posizione dell&#39;indicatore di riproduzione e l&#39;avanzamento degli annunci riportati potrebbero mostrare delle discontinuità.
