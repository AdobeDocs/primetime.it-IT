---
description: Il processo di inserimento video on-demand (VOD) consiste nelle fasi di risoluzione degli annunci, inserimento di annunci e riproduzione di annunci. Per il tracciamento degli annunci, TVSDK deve informare un server di tracciamento remoto dell'avanzamento della riproduzione di ciascun annuncio. In caso di situazioni impreviste, TVSDK esegue le azioni appropriate.
seo-description: Il processo di inserimento video on-demand (VOD) consiste nelle fasi di risoluzione degli annunci, inserimento di annunci e riproduzione di annunci. Per il tracciamento degli annunci, TVSDK deve informare un server di tracciamento remoto dell'avanzamento della riproduzione di ciascun annuncio. In caso di situazioni impreviste, TVSDK esegue le azioni appropriate.
seo-title: Inserimento pubblicitario e failover per VOD
title: Inserimento pubblicitario e failover per VOD
uuid: 1f813065-9310-4495-9fbb-d90eda8ac8bd
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Inserimento pubblicitario e failover per VOD {#advertising-insertion-and-failover-for-vod}

Il processo di inserimento video on-demand (VOD) consiste nelle fasi di risoluzione degli annunci, inserimento di annunci e riproduzione di annunci. Per il tracciamento degli annunci, TVSDK deve informare un server di tracciamento remoto dell&#39;avanzamento della riproduzione di ciascun annuncio. In caso di situazioni impreviste, TVSDK esegue le azioni appropriate.

## Fase di risoluzione degli annunci {#section_5DD3A7DA79E946298BFF829A60202E1C}

TVSDK contatta un servizio di distribuzione di annunci, come Adobe Primetime ad Decioning, e tenta di ottenere il file playlist principale che corrisponde al flusso video per l&#39;annuncio. Durante la fase di risoluzione degli annunci, TVSDK effettua una chiamata HTTP al server remoto di distribuzione degli annunci e analizza la risposta del server.

TVSDK supporta i seguenti tipi di provider di annunci:

* Metadati e provider

   I dati dell&#39;annuncio vengono codificati in file JSON in testo normale.
* Primetime e fornitore di annunci pubblicitari con decisione

   TVSDK invia una richiesta, inclusa una serie di parametri di targeting e un numero di identificazione della risorsa, al server di back-end Primetime e Decision. Primetime ad Decisioningrisponde con un documento SMIL (Synchronmultimedia integration Language) contenente le informazioni richieste per l&#39;annuncio.
* Fornitore di indicatori di annunci personalizzati

   Gestisce la situazione in cui gli annunci vengono masterizzati nel flusso, dal lato server. TVSDK non esegue l&#39;inserimento effettivo degli annunci, ma deve tenere traccia degli annunci inseriti sul lato server. Questo provider imposta i marcatori di annunci utilizzati da TVSDK per eseguire il tracciamento degli annunci.

Durante questa fase può verificarsi una delle seguenti situazioni di failover:

* Impossibile recuperare i dati perché, ad esempio, la mancanza di connettività o un errore lato server, come una risorsa, non è possibile trovare e così via.
* I dati sono stati recuperati, ma il formato non è valido.

   Ciò potrebbe verificarsi perché, ad esempio, l&#39;analisi dei dati in entrata non è riuscita.

TVSDK invia una notifica di avviso relativa all&#39;errore e continua l&#39;elaborazione.

## Fase di inserimento annunci {#section_29F7F7756C8B40B99AD4C3DD16B72B5B}

TVSDK inserisce nella timeline il contenuto alternativo (annunci) che corrisponde al contenuto principale.

Al termine della fase di risoluzione degli annunci, TVSDK dispone di un elenco ordinato di risorse pubblicitarie raggruppate in interruzioni di annunci. Ogni interruzione di annuncio viene posizionata sulla timeline del contenuto principale utilizzando un valore di ora iniziale espresso in millisecondi (ms). Ogni annuncio in un&#39;interruzione annuncio ha una proprietà di durata che è anche espressa in ms. Gli annunci in un&#39;interruzione di annuncio sono concatenati e, di conseguenza, la durata di un&#39;interruzione di annuncio è uguale alla somma delle durate dei singoli annunci che li compongono.

Il failover può verificarsi in questa fase con conflitti che potrebbero verificarsi sulla timeline durante l&#39;inserimento di annunci. Per combinazioni specifiche di valori di inizio/durata dell&#39;interruzione di annunci, i segmenti di annunci potrebbero sovrapporsi. Questa sovrapposizione si verifica quando l&#39;ultima parte di un&#39;interruzione di annuncio interseca l&#39;inizio del primo annuncio nell&#39;interruzione di annuncio successiva. In queste situazioni, TVSDK elimina l’interruzione annuncio successiva e continua il processo di inserimento annunci con la voce successiva nell’elenco fino a quando tutte le interruzioni di annuncio non vengono inserite o eliminate.

TVSDK invia una notifica di avviso relativa all&#39;errore e continua l&#39;elaborazione.

## Fase ad-riproduzione {#section_DA816F88AF8A4A5A8FD0DE2D54A86031}

TVSDK scarica i segmenti di annunci e li visualizza sullo schermo del dispositivo.

Ora, TVSDK ha risolto gli annunci, posizionato gli annunci sulla timeline e tenta di eseguire il rendering del contenuto sullo schermo.

Le seguenti classi principali di errori possono verificarsi nelle seguenti fasi:

* Quando ci si connette al server host.
* Quando si scarica il file manifesto.
* Quando si scaricano i segmenti multimediali.

TVSDK inoltra gli eventi attivati alla tua applicazione, compresi gli eventi di notifica attivati quando:

* Si verifica un failover.
* Il profilo viene modificato a causa dell&#39;algoritmo di failover.
* Sono state prese in considerazione tutte le opzioni di failover e non è possibile eseguire automaticamente alcuna azione aggiuntiva.

   La tua applicazione deve intraprendere l&#39;azione appropriata.

Indipendentemente dal verificarsi di errori, le chiamate TVSDK `onAdBreakComplete` per ogni `onAdBreakStart` e `onAdComplete` per ogni `onAdStart`. Tuttavia, se non è stato possibile scaricare i segmenti, potrebbero verificarsi degli spazi nella timeline. Quando gli spazi vuoti sono sufficientemente grandi, i valori nella posizione dell&#39;indicatore di riproduzione e l&#39;avanzamento degli annunci riportati potrebbero mostrare delle discontinuità.
