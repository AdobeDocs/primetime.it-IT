---
description: Il processo di inserimento degli annunci video-on-demand (VOD) consiste nelle fasi di risoluzione degli annunci, inserimento degli annunci e riproduzione degli annunci. Per il tracciamento degli annunci, il browser TVSDK deve informare un server di tracciamento remoto dell'avanzamento della riproduzione di ciascun annuncio. Quando si verificano situazioni impreviste, adotta le azioni appropriate.
title: Inserimento e failover della pubblicità per VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---


# Inserimento e failover della pubblicità per VOD{#advertising-insertion-and-failover-for-vod}

Il processo di inserimento degli annunci video-on-demand (VOD) consiste nelle fasi di risoluzione degli annunci, inserimento degli annunci e riproduzione degli annunci. Per il tracciamento degli annunci, il browser TVSDK deve informare un server di tracciamento remoto dell&#39;avanzamento della riproduzione di ciascun annuncio. Quando si verificano situazioni impreviste, adotta le azioni appropriate.

## Fase di risoluzione degli annunci {#section_F562CD6D0EF04AA9A0A3C0176A4EC340}

Il browser TVSDK contatta un servizio di distribuzione di annunci, come Adobe Primetime ad decision, e tenta di ottenere il file playlist principale che corrisponde al flusso video per l&#39;annuncio. Durante la fase di risoluzione degli annunci, Browser TVSDK effettua una chiamata HTTP al server remoto di consegna degli annunci e analizza la risposta del server.

Il browser TVSDK supporta i seguenti tipi di provider di annunci:

* Metadati e provider

   I dati dell’annuncio vengono codificati in file JSON in formato testo normale.
* Ad Decioning Adobe Primetime

   Browser TVSDK invia una richiesta, incluso un set di parametri di targeting e un numero di identificazione delle risorse, al server back-end Adobe Primetime e decisionale. Adobe Primetime ad Decioning risponde con un documento SMIL (sincronizzato multimedia integration language) che contiene le informazioni richieste per l&#39;annuncio.

   In questa fase può verificarsi una delle seguenti situazioni di failover:

   * Impossibile recuperare i dati per motivi quali mancanza di connettività o errore lato server, ad esempio non è possibile trovare una risorsa e così via.
   * I dati sono stati recuperati, ma il formato non è valido.

      Ciò potrebbe verificarsi perché, ad esempio, l’analisi dei dati in entrata non è riuscita.
   Il browser TVSDK invia una notifica di avviso relativa all’errore e continua l’elaborazione.

## Fase di inserimento annunci {#section_88A0E4FA12394717A9D85689BD11D59F}

Il browser TVSDK inserisce il contenuto alternativo (annunci) nella timeline che corrisponde al contenuto principale.

Al termine della fase di risoluzione degli annunci, il browser TVSDK dispone di un elenco ordinato di risorse di annunci raggruppate in interruzioni di annunci. Ogni interruzione pubblicitaria viene posizionata nella timeline del contenuto principale utilizzando un valore di tempo iniziale espresso in millisecondi (ms). Ogni annuncio in un&#39;interruzione pubblicitaria ha una proprietà di durata che è espressa anche in ms. Gli annunci in una pausa pubblicitaria vengono incatenati uno dopo l&#39;altro. Di conseguenza, la durata di un’interruzione pubblicitaria è uguale alla somma delle durate dei singoli annunci compositi.

Il failover può verificarsi in questa fase con conflitti che potrebbero verificarsi nella timeline durante l&#39;inserimento di annunci. Per combinazioni specifiche di valori di inizio/durata di un’interruzione pubblicitaria, i segmenti di annunci potrebbero sovrapporsi. La sovrapposizione si verifica quando l’ultima parte di un’interruzione pubblicitaria interseca l’inizio del primo annuncio nell’interruzione pubblicitaria successiva. In queste situazioni, il browser TVSDK elimina l’interruzione pubblicitaria successiva e continua il processo di inserimento degli annunci con la voce successiva nell’elenco fino a quando tutte le interruzioni di annunci non vengono inserite o scartate.

Il browser TVSDK invia una notifica di avviso relativa all’errore e continua l’elaborazione.

## Fase di riproduzione annunci {#section_7B0073BE9A744C74929263182C1243FC}

Il browser TVSDK scarica i segmenti di annunci e li riproduce sullo schermo del dispositivo.

A questo punto, Browser TVSDK ha risolto gli annunci, li ha posizionati sulla timeline e tenta di eseguire il rendering del contenuto sullo schermo.

In questa fase potrebbero verificarsi le seguenti principali classi di errori:

* Errori durante la connessione al server host
* Errori durante il download del file manifesto
* Errori durante il download dei segmenti multimediali

Per tutte e tre le classi di errore, Browser TVSDK inoltra gli eventi attivati all&#39;applicazione, tra cui:

* Eventi di notifica attivati quando si verifica un failover.
* Eventi di notifica quando il profilo viene modificato a causa dell&#39;algoritmo di failover.
* Eventi di notifica attivati quando sono state prese in considerazione tutte le opzioni di failover e non è possibile eseguire automaticamente alcuna azione aggiuntiva.

   La tua applicazione deve intraprendere l&#39;azione appropriata.

Che si verifichino o meno errori, il browser TVSDK vi notifica quando inizia un&#39;interruzione pubblicitaria e quando viene completata. Tuttavia, se non è stato possibile scaricare i segmenti, potrebbero esserci spazi nella timeline. Quando gli spazi vuoti sono sufficientemente grandi, i valori nella posizione della testina di riproduzione e l&#39;avanzamento dell&#39;annuncio riportato potrebbero presentare delle discontinuità.
