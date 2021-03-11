---
description: I componenti principali di Adobe Access sono costituiti da un SDK Java e dagli ambienti runtime client Flash Player e Adobe AIR.
title: Client SDK Java, Flash Player e Adobe AIR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---


# Adobe Access components{#adobe-access-components}

I componenti principali di Adobe Access sono costituiti da un SDK Java e dagli ambienti runtime client Flash Player e Adobe AIR.

Per ulteriori informazioni sulla configurazione dell&#39;SDK, consulta Configurazione dell&#39;SDK in *Utilizzo dell&#39;SDK per l&#39;accesso Adobe per la protezione dei contenuti.*

L’SDK di Adobe Access consente di sviluppare una soluzione di gestione dei diritti digitali che si integra con l’infrastruttura aziendale esistente della tua organizzazione, ad esempio i sistemi di gestione dei contenuti, fatturazione e controllo degli accessi utente. Flash Player e Adobe AIR consentono di creare e distribuire facilmente applicazioni attraverso le quali i consumatori possono accedere e visualizzare grandi librerie di contenuti digitali.

## Adobe Access SDK {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe Access viene fornito come SDK Java che fornisce i blocchi predefiniti da cui puoi creare un’implementazione del server. Con l’SDK puoi creare una soluzione di accesso Adobe adatta al modello aziendale della tua organizzazione.

Le API Java fornite nell’SDK sono descritte nelle seguenti sottosezioni.

## API Java per la gestione dei domini dei gruppi di dispositivi {#java-apis-for-managing-device-group-domains}

Queste API vengono utilizzate per consentire al server di gestire le richieste client per l’unione e l’uscita dai domini del gruppo di dispositivi.

Un dominio di gruppo di dispositivi è una raccolta logica di dispositivi in grado di condividere licenze tra loro. Affinché ciò accada, ogni dispositivo deve prima iscriversi/registrarsi allo stesso dominio. L’SDK di Adobe Access, in esecuzione su un server, deve gestire le richieste di unione (registrazione) di Device Domain, nonché le richieste di congedo (de-register) di Device Domain. Ai dispositivi che non fanno parte di alcun dominio verranno rilasciate licenze associate a tale dispositivo, che non possono essere condivise con nessun altro dispositivo.

## API Java per la protezione dei contenuti {#java-apis-for-protecting-content}

Queste API vengono utilizzate per definire i diritti e preparare i contenuti per la distribuzione. Le API di protezione dei contenuti sono:

* Gestione dei criteri

   L’API di gestione dei criteri viene utilizzata per creare e modificare i criteri da applicare ai contenuti. I criteri possono essere creati o aggiornati, comprese le informazioni su come ottenere/impostare tutte le regole di utilizzo e consentire l’utilizzo di parametri aggiuntivi in uno spazio dei nomi personalizzato.

* Pacchetto di contenuti

   L’API per la creazione di pacchetti di contenuti viene utilizzata per crittografare i contenuti e recuperare i metadati dal contenuto in pacchetto.

## API Java per il rilascio di licenze {#java-apis-for-issuing-licenses}

Queste API vengono utilizzate quando un client richiede una licenza dal server. L&#39;SDK supporta le seguenti richieste dal client:

* Autenticazione

   L’API di autenticazione può essere utilizzata per gestire le richieste di autenticazione e generare token di autenticazione.

* Generazione e acquisizione di licenze

   L’API di generazione e acquisizione della licenza viene utilizzata per generare una licenza per l’utente.

* Supporto per client e contenuti Adobe AIR versione 1.5

   Ai fini della compatibilità con le versioni precedenti, l’SDK dispone di API per gestire le richieste di applicazioni AIR create per l’utilizzo con AIR versione 1.5 e precedenti e contenuti protetti.

## Implementazione di riferimento {#reference-implementation}

L&#39;SDK include un&#39;implementazione di riferimento, una semplice implementazione di Adobe Access che illustra come utilizzare le API Java. L&#39;implementazione di riferimento fornisce un License Server, Watched Folder Packager, Adobe Access Manager AIR application e strumenti da riga di comando per la creazione di pacchetti di contenuti e la gestione dei criteri in base alle API Java. Per ulteriori informazioni sull&#39;implementazione di riferimento di Adobe Access, consulta *Protezione dei contenuti*.

## Adobe Access Server per streaming protetto {#adobe-access-server-for-protected-streaming}

Per i casi di utilizzo in streaming in cui il contenuto è protetto con accesso Adobe, ad Adobe HTTP Dynamic Streaming, il software include anche Adobe Access Server for Protected Streaming. Questa soluzione può essere facilmente implementata su un contenitore servlet come Tomcat e può raggiungere un alto livello di scalabilità e prestazioni per soddisfare le più grandi esigenze di distribuzione dei contenuti.

## Flash Player Adobe {#adobe-flash-player}

Flash Player è un plug-in e runtime del browser leggero che offre esperienze utente coerenti e coinvolgenti, straordinaria riproduzione audio/video e portata dilagante. Il Flash Player offre una riproduzione di alta qualità dei contenuti video in streaming o scaricati. Per gli editori di contenuti, Flash Player offre gli strumenti per personalizzare gli schermi di riproduzione che circondano i contenuti, consentendo esperienze di branding più approfondite e monetizzazione attraverso la pubblicità tramite banner e sovrapposizioni. Per i consumatori, il Flash Player offre un modo intuitivo e visivo di visualizzare i contenuti video.

Per ulteriori informazioni sul Flash Player, visita: [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR è un runtime di sistema interoperativo che consente ai produttori di contenuti di estendere i loro investimenti esistenti nel web al desktop progettando applicazioni multimediali personalizzate. Basato su tecnologie aperte e comprovate, offre alle aziende un modo affidabile e semplificato di sviluppare e distribuire applicazioni personalizzate che possono essere affidabili per offrire un&#39;esperienza utente più sicura e piacevole. Adobe AIR consente alle aziende di integrare facilmente i rich media per creare un’esperienza utente più coinvolgente e interattiva. Consente agli sviluppatori di utilizzare strumenti familiari come HTML, JavaScript, Flash o il software Adobe® Flex® per implementare la combinazione unica di applicazioni Internet avanzate in Windows, Macintosh o Linux.

Le aziende hanno il controllo completo dell&#39;interfaccia utente e possono progettare un&#39;esperienza utente per riflettere e rafforzare il proprio marchio. Grazie al supporto integrato per la riproduzione di contenuti protetti con Adobe Access SDK, Adobe AIR consente di creare catene di distribuzione dei contenuti end-to-end personalizzate.

Per ulteriori informazioni su Adobe AIR, visita: [www.adobe.com/go/air](https://www.adobe.com/go/air)

## Applicazioni native per iOS e Android {#native-ios-and-android-applications}

Applicazioni native per iOS e Android Disponibile solo per i clienti Adobe Primetime, Adobe Access DRM 4.0 e versioni successive può essere utilizzato per proteggere i video utilizzati nelle applicazioni native (non di Flash) su dispositivi mobili. Affinché un&#39;applicazione utilizzi questo contenuto protetto, è necessario implementarlo utilizzando le librerie client di Adobe Primetime.

Per ulteriori informazioni su Adobe Primetime, visita: [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)