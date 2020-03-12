---
description: I componenti principali di Adobe Access sono costituiti da un Java SDK e dagli ambienti runtime client Flash Player e Adobe AIR.
seo-description: I componenti principali di Adobe Access sono costituiti da un Java SDK e dagli ambienti runtime client Flash Player e Adobe AIR.
seo-title: Java SDK, Flash Player e il client Adobe AIR
title: Java SDK, Flash Player e il client Adobe AIR
uuid: 6b6c5aa2-56ee-4476-a05b-dcbbe3b9001e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Componenti di Adobe Access{#adobe-access-components}

I componenti principali di Adobe Access sono costituiti da un Java SDK e dagli ambienti runtime client Flash Player e Adobe AIR.

Per ulteriori informazioni sulla configurazione dell’SDK, consulta Configurazione dell’SDK in *Utilizzo di Adobe Access SDK per la protezione dei contenuti.*

L’SDK di Adobe Access consente di sviluppare una soluzione di gestione dei diritti digitali che si integri con l’infrastruttura aziendale esistente della tua organizzazione, come la gestione dei contenuti, la fatturazione e i sistemi di controllo degli accessi utente. Flash Player e Adobe AIR consentono di creare e distribuire facilmente applicazioni attraverso le quali i consumatori possono accedere e visualizzare grandi librerie di contenuti digitali.

## Adobe Access SDK {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe Access viene fornito come SDK Java che fornisce i blocchi costitutivi dai quali è possibile creare un&#39;implementazione del server. Con l’SDK puoi creare una soluzione Adobe Access adatta al modello aziendale dell’organizzazione.

Le API Java fornite nell’SDK sono descritte nelle seguenti sottosezioni.

## API Java per la gestione dei domini dei gruppi di dispositivi {#java-apis-for-managing-device-group-domains}

Queste API vengono utilizzate per consentire al server di gestire le richieste client per l&#39;adesione e l&#39;uscita dai domini dei gruppi di dispositivi.

Un dominio di gruppo di dispositivi è una raccolta logica di dispositivi in grado di condividere le licenze tra loro. Affinché ciò possa avvenire, ogni dispositivo deve prima registrarsi o registrarsi nello stesso dominio. L&#39;SDK di Adobe Access, in esecuzione su un server, deve gestire le richieste di partecipazione (registrazione) del dominio dispositivo e le richieste di congedo (deregistrazione) del dominio dispositivo. Ai dispositivi che non fanno parte di un dominio verranno rilasciate licenze associate a tale dispositivo, che non possono essere condivise con altri dispositivi.

## API Java per la protezione del contenuto {#java-apis-for-protecting-content}

Queste API vengono utilizzate per definire i diritti e preparare il contenuto per la distribuzione. Le API per la protezione del contenuto sono:

* Gestione dei criteri

   L&#39;API di gestione criteri viene utilizzata per creare e modificare i criteri da applicare al contenuto. I criteri possono essere creati o aggiornati, incluso ottenere/impostare tutte le regole di utilizzo e consentire parametri aggiuntivi in uno spazio dei nomi personalizzato.

* Creazione di contenuti

   L&#39;API per la creazione di pacchetti di contenuto viene utilizzata per cifrare il contenuto e recuperare i metadati dal contenuto incluso nel pacchetto.

## API Java per il rilascio di licenze {#java-apis-for-issuing-licenses}

Queste API vengono utilizzate quando un client richiede una licenza dal server. L’SDK supporta le seguenti richieste dal client:

* Autenticazione

   L&#39;API di autenticazione può essere utilizzata per gestire le richieste di autenticazione e generare token di autenticazione.

* Generazione e acquisizione di licenze

   L&#39;API di generazione e acquisizione della licenza viene utilizzata per generare una licenza per l&#39;utente.

* Supporto per client e contenuti Adobe AIR versione 1.5

   Ai fini della compatibilità con le versioni precedenti, l’SDK dispone di API per gestire le richieste delle applicazioni AIR create per l’uso con i client AIR versione 1.5 e versioni precedenti e il contenuto protetto.

## Implementazione di riferimento {#reference-implementation}

L&#39;SDK include un&#39;implementazione di riferimento, una semplice distribuzione di Adobe Access che illustra come utilizzare le API Java. L&#39;implementazione di riferimento fornisce un server licenze, un pacchetto cartelle esaminate, un&#39;applicazione AIR Adobe Access Manager e strumenti della riga di comando per la creazione di pacchetti di contenuto e la gestione dei criteri basati sulle API Java. Per ulteriori informazioni sull&#39;implementazione di riferimento di Adobe Access, consulta *Protezione dei contenuti*.

## Adobe Access Server per lo streaming protetto {#adobe-access-server-for-protected-streaming}

Per i casi di utilizzo in streaming in cui il contenuto è protetto con Adobe Access, ad esempio per Adobe HTTP Dynamic Streaming, il software include anche Adobe Access Server for Protected Streaming. Questa soluzione può essere facilmente implementata su un contenitore servlet come Tomcat e può raggiungere un alto livello di scalabilità e prestazioni per soddisfare le più grandi esigenze di distribuzione dei contenuti.

## Adobe Flash Player {#adobe-flash-player}

Flash Player è un plug-in e un runtime per browser leggeri che offre esperienze utente coerenti e coinvolgenti, una straordinaria riproduzione audio/video e una portata molto ampia. Flash Player offre una riproduzione di alta qualità dei contenuti video in streaming o scaricati. Per gli editori di contenuti, Flash Player offre gli strumenti per personalizzare gli schermi di riproduzione che circondano i contenuti, consentendo esperienze di branding più profonde e la monetizzazione attraverso la pubblicità tramite banner e sovrapposizioni. Per i consumatori, Flash Player offre un modo intuitivo e visivo per visualizzare i contenuti video.

Per ulteriori informazioni su Flash Player, visitate: [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR è un runtime basato su più sistemi operativi che consente ai produttori di contenuti di estendere gli investimenti esistenti nel Web al desktop progettando applicazioni multimediali personalizzate. Basato su tecnologie collaudate e aperte, offre alle aziende un modo affidabile e semplificato di sviluppare e implementare applicazioni personalizzate che possono essere affidabili per offrire un&#39;esperienza utente più sicura e piacevole. Adobe AIR consente alle aziende di integrare facilmente i contenuti multimediali per creare un&#39;esperienza utente interattiva e più coinvolgente. Consente agli sviluppatori di utilizzare strumenti familiari come HTML, JavaScript, Flash o Adobe® Flex® per implementare la combinazione unica di applicazioni Internet avanzate in Windows, Macintosh o Linux.

Le aziende hanno il controllo completo dell&#39;interfaccia utente e possono progettare un&#39;esperienza utente che rifletta e rafforzi il proprio marchio. Grazie al supporto integrato per la riproduzione di contenuto protetto con Adobe Access SDK, Adobe AIR consente di creare catene di distribuzione di contenuti end-to-end personalizzate.

Per ulteriori informazioni su Adobe AIR, visitate: [www.adobe.com/go/air](https://www.adobe.com/go/air)

## Applicazioni iOS e Android native {#native-ios-and-android-applications}

Le applicazioni iOS e Android native, disponibili solo per i clienti Adobe Primetime, Adobe Access DRM 4.0 e versioni successive, possono essere utilizzate per proteggere i video utilizzati nelle applicazioni native (non Flash) sui dispositivi mobili. Affinché un&#39;applicazione utilizzi questo contenuto protetto, è necessario implementarlo utilizzando le librerie client Adobe Primetime.

Per maggiori informazioni su Adobe Primetime, visita: [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)