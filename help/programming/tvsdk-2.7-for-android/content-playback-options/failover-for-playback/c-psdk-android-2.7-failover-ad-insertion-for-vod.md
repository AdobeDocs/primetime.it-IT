---
description: Il processo di inserimento di annunci video-on-demand (VOD) è costituito dalle fasi di risoluzione, inserimento e riproduzione degli annunci. Per il tracciamento degli annunci, TVSDK deve informare un server di tracciamento remoto sull’avanzamento della riproduzione di ciascun annuncio. In caso di situazioni impreviste, TVSDK adotta le misure appropriate.
title: Inserimento e failover di annunci per VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---

# Inserimento e failover di annunci per VOD {#advertising-insertion-and-failover-for-vod}

Il processo di inserimento di annunci video-on-demand (VOD) è costituito dalle fasi di risoluzione, inserimento e riproduzione degli annunci. Per il tracciamento degli annunci, TVSDK deve informare un server di tracciamento remoto sull’avanzamento della riproduzione di ciascun annuncio. In caso di situazioni impreviste, TVSDK adotta le misure appropriate.

## Fase di risoluzione degli annunci {#section_5DD3A7DA79E946298BFF829A60202E1C}

TVSDK contatta un servizio di consegna degli annunci, come Adobe Primetime ad decisioning, e tenta di ottenere il file della playlist principale che corrisponde al flusso video per l’annuncio. Durante la fase di risoluzione degli annunci, TVSDK effettua una chiamata HTTP al server di consegna degli annunci remoto e analizza la risposta del server.

TVSDK supporta i seguenti tipi di provider di annunci:

* Provider di annunci metadati

  I dati dell’annuncio sono codificati in file JSON di testo normale.
* Provider di annunci di Ad Decisioning di Primetime

  TVSDK invia una richiesta, contenente un set di parametri di targeting e un numero di identificazione della risorsa, al server back-end Primetime ad decisioning. Primetime ad decisioningrisponde con un documento SMIL (Synchronized Multimedia Integration Language) contenente le informazioni sull’annuncio richieste.
* Provider di marcatori annunci personalizzati

  Gestisce la situazione in cui gli annunci vengono masterizzati nel flusso, dal lato server. TVSDK non esegue l’inserimento effettivo dell’annuncio, ma deve tenere traccia degli annunci inseriti sul lato server. Questo provider imposta i marcatori annuncio utilizzati da TVSDK per eseguire il tracciamento degli annunci.

Durante questa fase può verificarsi una delle seguenti situazioni di failover:

* Non è possibile recuperare i dati a causa, ad esempio, della mancanza di connettività o di un errore sul lato server, ad esempio l’impossibilità di trovare una risorsa e così via.
* I dati sono stati recuperati, ma il formato non è valido.

  Ciò potrebbe verificarsi, ad esempio, perché l’analisi dei dati in entrata non è riuscita.

TVSDK invia una notifica di avviso relativa all’errore e continua l’elaborazione.

## Fase di inserimento dell’annuncio {#section_29F7F7756C8B40B99AD4C3DD16B72B5B}

TVSDK inserisce il contenuto alternativo (annunci) nella timeline che corrisponde al contenuto principale.

Al termine della fase di risoluzione degli annunci, TVSDK dispone di un elenco ordinato di risorse pubblicitarie raggruppate in interruzioni pubblicitarie. Ogni interruzione pubblicitaria viene posizionata sulla timeline del contenuto principale utilizzando un valore di ora di inizio espresso in millisecondi (ms). Ogni annuncio in un’interruzione pubblicitaria ha una proprietà duration espressa anche in ms. Gli annunci in un’interruzione pubblicitaria sono concatenati e, di conseguenza, la durata di un’interruzione pubblicitaria è pari alla somma delle durate dei singoli annunci di composizione.

In questa fase può verificarsi il failover con conflitti che potrebbero verificarsi sulla timeline durante l’inserimento di annunci. Per combinazioni specifiche di valori di ora di inizio/durata dell’interruzione pubblicitaria, i segmenti dell’annuncio potrebbero sovrapporsi. Questa sovrapposizione si verifica quando l’ultima parte di un’interruzione pubblicitaria interseca l’inizio del primo annuncio nell’interruzione pubblicitaria successiva. In queste situazioni, TVSDK elimina l’interruzione pubblicitaria successiva e continua il processo di inserimento dell’annuncio con la voce successiva nell’elenco fino a quando tutte le interruzioni pubblicitarie non vengono inserite o eliminate.

TVSDK invia una notifica di avviso relativa all’errore e continua l’elaborazione.

## Fase riproduzione annuncio {#section_DA816F88AF8A4A5A8FD0DE2D54A86031}

TVSDK scarica i segmenti dell’annuncio ed esegue il rendering sullo schermo del dispositivo.

Ora TVSDK ha risolto gli annunci, posizionato gli annunci sulla timeline e tenta di eseguire il rendering del contenuto sullo schermo.

Le seguenti classi principali di errori possono verificarsi durante le fasi seguenti:

* Durante la connessione al server host.
* Quando si scarica il file manifesto.
* Durante il download dei segmenti multimediali.

TVSDK inoltra gli eventi attivati all&#39;applicazione, inclusi gli eventi di notifica che vengono attivati quando:

* Si verifica un failover.
* Il profilo viene modificato a causa dell&#39;algoritmo di failover.
* Sono state prese in considerazione tutte le opzioni di failover e non è possibile eseguire automaticamente alcuna azione aggiuntiva.

  L&#39;applicazione deve intraprendere l&#39;azione appropriata.

Indipendentemente dal fatto che si verifichino errori, chiamate TVSDK `onAdBreakComplete` per ogni `onAdBreakStart` e `onAdComplete` per ogni `onAdStart`. Tuttavia, se non è stato possibile scaricare i segmenti, potrebbero esserci degli spazi nella timeline. Quando gli spazi sono sufficientemente ampi, i valori nella posizione della testina di riproduzione e l’avanzamento dell’annuncio riportato potrebbero mostrare discontinuità.
