---
description: Il processo di inserimento di annunci video-on-demand (VOD) è costituito dalle fasi di risoluzione, inserimento e riproduzione degli annunci. Per il tracciamento degli annunci, TVSDK deve informare un server di tracciamento remoto sull’avanzamento della riproduzione di ciascun annuncio. Quando si verificano situazioni impreviste, adotta le misure appropriate.
title: Inserimento e failover di annunci per VOD
exl-id: 5af5bef6-e948-4215-a89f-ee46fd2d8a38
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# Inserimento e failover di annunci per VOD{#advertising-insertion-and-failover-for-vod}

Il processo di inserimento di annunci video-on-demand (VOD) è costituito dalle fasi di risoluzione, inserimento e riproduzione degli annunci. Per il tracciamento degli annunci, TVSDK deve informare un server di tracciamento remoto sull’avanzamento della riproduzione di ciascun annuncio. Quando si verificano situazioni impreviste, adotta le misure appropriate.

## Fase di risoluzione degli annunci {#section_0D45C6094D724B55868B48F9A3557A8B}

TVSDK contatta un servizio di consegna degli annunci, come Adobe Primetime ad decisioning, e tenta di ottenere il file della playlist principale che corrisponde al flusso video per l’annuncio. Durante la fase di risoluzione degli annunci, TVSDK effettua una chiamata HTTP al server di consegna degli annunci remoto e analizza la risposta del server.

TVSDK supporta i seguenti tipi di provider di annunci:

* Provider di annunci metadati

   I dati dell’annuncio sono codificati in file JSON di testo normale.
* Provider di annunci di Ad Decisioning di Primetime

   TVSDK invia una richiesta, contenente un set di parametri di targeting e un numero di identificazione della risorsa, al server back-end di Primetime ad decisioning. Primetime ad decisioning risponde con un documento SMIL (Synchronized Multimedia Integration Language) contenente le informazioni sull’annuncio richieste.

Durante questa fase può verificarsi una delle seguenti situazioni di failover:

* Non è possibile recuperare i dati per motivi quali mancanza di connettività o errore lato server, ad esempio l’impossibilità di trovare una risorsa e così via.
* I dati sono stati recuperati, ma il formato non è valido.

   Ciò potrebbe verificarsi, ad esempio, perché l’analisi dei dati in entrata non è riuscita.

TVSDK invia una notifica di avviso relativa all’errore e continua l’elaborazione.

## Fase di inserimento dell’annuncio {#section_1B18E8B5768B4873B3346294175B7340}

TVSDK inserisce il contenuto alternativo (annunci) nella timeline che corrisponde al contenuto principale.

Al termine della fase di risoluzione degli annunci, TVSDK dispone di un elenco ordinato di risorse pubblicitarie raggruppate in interruzioni pubblicitarie. Ogni interruzione pubblicitaria è posizionata sulla timeline del contenuto principale utilizzando un valore di ora di inizio espresso in millisecondi (ms). Ogni annuncio in un’interruzione pubblicitaria ha una proprietà duration espressa anche in ms. Gli annunci in un’interruzione pubblicitaria sono concatenati uno dopo l’altro. Di conseguenza, la durata di un’interruzione pubblicitaria è uguale alla somma delle durate dei singoli annunci di composizione.

In questa fase può verificarsi il failover con conflitti che potrebbero verificarsi sulla timeline durante l’inserimento di annunci. Per combinazioni specifiche di valori di ora di inizio/durata dell’interruzione pubblicitaria, i segmenti dell’annuncio potrebbero sovrapporsi. La sovrapposizione si verifica quando l’ultima parte di un’interruzione pubblicitaria interseca l’inizio del primo annuncio nell’interruzione pubblicitaria successiva. In queste situazioni, elimina l’interruzione pubblicitaria successiva e continua il processo di inserimento dell’annuncio con l’elemento successivo nell’elenco fino a quando tutte le interruzioni pubblicitarie non vengono inserite o eliminate.

TVSDK invia una notifica di avviso relativa all’errore e continua l’elaborazione.

## Fase riproduzione annuncio {#section_64777BD2CDA84EACB0A4EA6D68367CF5}

TVSDK scarica i segmenti dell’annuncio ed esegue il rendering sullo schermo del dispositivo.

A questo punto, TVSDK ha risolto gli annunci, li ha posizionati sulla timeline e tenta di eseguire il rendering del contenuto sullo schermo.

In questa fase possono verificarsi le seguenti classi principali di errori:

* Errori durante la connessione al server host
* Errori durante il download del file manifesto
* Errori durante il download dei segmenti multimediali

Per tutte e tre le classi di errore, TVSDK inoltra gli eventi attivati all’applicazione, tra cui:

* Eventi di notifica attivati quando si verifica un failover.
* Eventi di notifica quando il profilo viene modificato a causa dell’algoritmo di failover.
* Gli eventi di notifica vengono attivati quando tutte le opzioni di failover sono state considerate e non è possibile eseguire alcuna azione aggiuntiva automaticamente.

   L&#39;applicazione deve intraprendere l&#39;azione appropriata.

Se si verificano o meno errori, chiamate TVSDK `AdBreakPlaybackEvent.AD_BREAK_COMPLETE` per ogni `AdBreakPlaybackEvent.AD_BREAK_STARTED` e `AdPlaybackEvent.AD_COMPLETED` per ogni `AdPLaybackEvent.AD_STARTED`. Tuttavia, se non è stato possibile scaricare i segmenti, potrebbero esserci degli spazi nella timeline. Quando gli spazi sono sufficientemente ampi, i valori nella posizione della testina di riproduzione e l’avanzamento dell’annuncio riportato potrebbero mostrare discontinuità.
