---
description: Il processo di inserimento degli annunci video-on-demand (VOD) consiste nelle fasi di risoluzione degli annunci, inserimento degli annunci e riproduzione degli annunci. Per il tracciamento degli annunci, TVSDK deve informare un server di tracciamento remoto dell’avanzamento della riproduzione di ciascun annuncio. In caso di situazioni impreviste, TVSDK esegue le azioni appropriate.
title: Inserimento e failover della pubblicità per VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 0%

---


# Inserimento e failover della pubblicità per VOD {#advertising-insertion-and-failover-for-vod}

Il processo di inserimento degli annunci video-on-demand (VOD) consiste nelle fasi di risoluzione degli annunci, inserimento degli annunci e riproduzione degli annunci. Per il tracciamento degli annunci, TVSDK deve informare un server di tracciamento remoto dell’avanzamento della riproduzione di ciascun annuncio. In caso di situazioni impreviste, TVSDK esegue le azioni appropriate.

## Fase di risoluzione degli annunci {#section_5DD3A7DA79E946298BFF829A60202E1C}

TVSDK contatta un servizio di consegna annunci, come Adobe Primetime ad decision, e tenta di ottenere il file playlist principale che corrisponde al flusso video per l&#39;annuncio. Durante la fase di risoluzione degli annunci, TVSDK effettua una chiamata HTTP al server remoto di consegna degli annunci e analizza la risposta del server.

TVSDK supporta i seguenti tipi di provider di annunci:

* Metadati e provider

   I dati dell’annuncio vengono codificati in file JSON in formato testo normale.
* Primetime ad decision provider

   TVSDK invia una richiesta, incluso un set di parametri di targeting e un numero di identificazione della risorsa, al server di back-end Primetime ad decision. Primetime ad decision risponde con un documento SMIL (sincronizzato multimedia integration language) che contiene le informazioni richieste per l&#39;annuncio.
* Fornitore di indicatori di annunci personalizzati

   Gestisce la situazione in cui gli annunci vengono bruciati nel flusso, dal lato server. TVSDK non esegue l’inserimento effettivo degli annunci, ma deve tenere traccia degli annunci inseriti sul lato server. Questo provider imposta i marcatori di annunci utilizzati da TVSDK per eseguire il tracciamento degli annunci.

In questa fase può verificarsi una delle seguenti situazioni di failover:

* Impossibile recuperare i dati perché, ad esempio, la connettività è insufficiente o si è verificato un errore lato server, ad esempio una risorsa non trovata e così via.
* I dati sono stati recuperati, ma il formato non è valido.

   Ciò potrebbe verificarsi perché, ad esempio, l’analisi dei dati in entrata non è riuscita.

TVSDK invia una notifica di avviso relativa all’errore e continua l’elaborazione.

## Fase di inserimento annunci {#section_29F7F7756C8B40B99AD4C3DD16B72B5B}

TVSDK inserisce il contenuto alternativo (annunci) nella timeline che corrisponde al contenuto principale.

Al termine della fase di risoluzione degli annunci, TVSDK dispone di un elenco ordinato di risorse di annunci raggruppate in interruzioni di annunci. Ogni interruzione pubblicitaria è posizionata nella timeline del contenuto principale utilizzando un valore di inizio tempo espresso in millisecondi (ms). Ogni annuncio in un&#39;interruzione pubblicitaria ha una proprietà di durata che è espressa anche in ms. Gli annunci in un’interruzione pubblicitaria sono concatenati e, di conseguenza, la durata di un’interruzione pubblicitaria è uguale alla somma delle durate dei singoli annunci compositi.

Il failover può verificarsi in questa fase con conflitti che potrebbero verificarsi nella timeline durante l&#39;inserimento degli annunci. Per combinazioni specifiche di valori di inizio/durata di un’interruzione pubblicitaria, i segmenti di annunci potrebbero sovrapporsi. Questa sovrapposizione si verifica quando l’ultima parte di un’interruzione pubblicitaria interseca l’inizio del primo annuncio nell’interruzione pubblicitaria successiva. In queste situazioni, TVSDK elimina l’interruzione pubblicitaria successiva e continua il processo di inserimento degli annunci con la voce successiva nell’elenco fino a quando tutte le interruzioni di annunci non vengono inserite o scartate.

TVSDK invia una notifica di avviso relativa all’errore e continua l’elaborazione.

## Fase di riproduzione annunci {#section_DA816F88AF8A4A5A8FD0DE2D54A86031}

TVSDK scarica i segmenti di annunci ed effettua il rendering sullo schermo del dispositivo.

Ora, TVSDK ha risolto gli annunci, posizionato gli annunci sulla timeline e tenta di eseguire il rendering del contenuto sullo schermo.

Le seguenti principali classi di errori possono verificarsi nelle seguenti fasi:

* Quando ci si connette al server host.
* Quando si scarica il file manifesto.
* Quando si scaricano i segmenti multimediali.

TVSDK inoltra gli eventi attivati alla tua applicazione, compresi gli eventi di notifica attivati quando:

* Si verifica un failover.
* Il profilo viene modificato a causa dell&#39;algoritmo di failover.
* Tutte le opzioni di failover sono state prese in considerazione e non è possibile eseguire automaticamente alcuna azione aggiuntiva.

   La tua applicazione deve intraprendere l&#39;azione appropriata.

Indipendentemente dal verificarsi degli errori, le chiamate TVSDK `onAdBreakComplete` per ogni `onAdBreakStart` e `onAdComplete` per ogni `onAdStart`. Tuttavia, se non è stato possibile scaricare i segmenti, potrebbero esserci spazi nella timeline. Quando gli spazi vuoti sono sufficientemente grandi, i valori nella posizione della testina di riproduzione e l&#39;avanzamento dell&#39;annuncio riportato potrebbero presentare delle discontinuità.
