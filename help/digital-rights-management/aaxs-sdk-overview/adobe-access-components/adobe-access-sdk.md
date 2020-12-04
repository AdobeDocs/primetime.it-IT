---
description: I componenti principali di  Adobe Access sono costituiti da un SDK Java e dagli ambienti runtime client Adobe AIR e di Flash Player e .
seo-description: I componenti principali di  Adobe Access sono costituiti da un SDK Java e dagli ambienti runtime client Adobe AIR e di Flash Player e .
seo-title: 'Java SDK, Flash Player e client Adobe AIR '
title: 'Java SDK, Flash Player e client Adobe AIR '
uuid: 6b6c5aa2-56ee-4476-a05b-dcbbe3b9001e
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


#  componenti Accesso Adobe{#adobe-access-components}

I componenti principali di  Adobe Access sono costituiti da un SDK Java e dagli ambienti runtime client Adobe AIR e di Flash Player e .

Per ulteriori informazioni sulla configurazione dell&#39;SDK, consulta Configurazione dell&#39;SDK in *Utilizzo dell&#39;SDK di accesso al Adobe  per la protezione dei contenuti.*

L’SDK per l’accesso ai Adobi  consente di sviluppare una soluzione di gestione dei diritti digitali che si integri con l’infrastruttura aziendale esistente, ad esempio i sistemi di gestione dei contenuti, fatturazione e controllo degli accessi utente. Adobe AIR e i Flash Player consentono di creare e distribuire facilmente applicazioni attraverso le quali i consumatori possono accedere e visualizzare grandi librerie di contenuti digitali.

##  Adobe Access SDK {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

 Accesso Adobe viene fornito come SDK Java che fornisce i blocchi costitutivi dai quali è possibile creare un&#39;implementazione del server. Con l’SDK potete creare una soluzione di accesso al Adobe  adatta al modello aziendale dell’organizzazione.

Le API Java fornite nell’SDK sono descritte nelle seguenti sottosezioni.

## API Java per la gestione dei domini dei gruppi di dispositivi {#java-apis-for-managing-device-group-domains}

Queste API vengono utilizzate per consentire al server di gestire le richieste client per l&#39;adesione e l&#39;uscita dai domini dei gruppi di dispositivi.

Un dominio di gruppo di dispositivi è una raccolta logica di dispositivi in grado di condividere le licenze tra loro. Affinché ciò possa avvenire, ogni dispositivo deve prima registrarsi o registrarsi nello stesso dominio. L&#39;SDK di accesso al Adobe , in esecuzione su un server, deve gestire le richieste di partecipazione (registrazione) a Device Domain, nonché le richieste di congedo (de-register) da Device Domain. Ai dispositivi che non fanno parte di un dominio verranno rilasciate licenze associate a tale dispositivo, che non possono essere condivise con altri dispositivi.

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

* Supporto per  client e contenuti Adobe AIR versione 1.5

   Ai fini della compatibilità con le versioni precedenti, l’SDK dispone di API per gestire le richieste delle applicazioni AIR create per l’uso con i client AIR versione 1.5 e versioni precedenti e il contenuto protetto.

## Implementazione di riferimento {#reference-implementation}

L’SDK include un’implementazione di riferimento, una semplice distribuzione di accesso  Adobe che illustra come utilizzare le API Java. L&#39;implementazione di riferimento fornisce un server licenze, un pacchetto cartelle esaminate, un&#39;applicazione AIR  Adobe Access Manager e strumenti della riga di comando per la creazione di pacchetti di contenuto e la gestione dei criteri basati sulle API Java. Per ulteriori informazioni sull&#39;implementazione di riferimento di Accesso  Adobe, vedere *Protezione dei contenuti*.

## Adobe Access Server per lo streaming protetto {#adobe-access-server-for-protected-streaming}

Per i casi di utilizzo in streaming in cui il contenuto è protetto con accesso  Adobe, ad esempio per  Adobe HTTP Dynamic Streaming, il software include anche Adobe Access Server per lo streaming protetto. Questa soluzione può essere facilmente implementata su un contenitore servlet come Tomcat e può raggiungere un alto livello di scalabilità e prestazioni per soddisfare le più grandi esigenze di distribuzione dei contenuti.

## Flash Player Adobe  {#adobe-flash-player}

Il Flash Player è un plug-in e un runtime per browser leggeri che offre esperienze utente coerenti e coinvolgenti, una straordinaria riproduzione audio/video e una portata molto ampia. Il Flash Player offre una riproduzione di alta qualità dei contenuti video in streaming o scaricati. Per gli editori di contenuti, il Flash Player offre gli strumenti per personalizzare gli schermi di riproduzione che circondano i contenuti, consentendo esperienze di branding più approfondite e monetizzazione attraverso la pubblicità tramite banner e sovrapposizioni. Per i consumatori, l&#39;Flash Player offre un modo intuitivo e visivo per visualizzare i contenuti video.

Per maggiori informazioni sul Flash Player, visita: [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

##  Adobe AIR {#adobe-air}

 Adobe AIR è un runtime basato su sistemi operativi diversi che consente ai produttori di contenuti di estendere gli investimenti esistenti sul Web al desktop progettando applicazioni multimediali personalizzate. Basato su tecnologie collaudate e aperte, offre alle aziende un modo affidabile e semplificato di sviluppare e implementare applicazioni personalizzate che possono essere affidabili per offrire un&#39;esperienza utente più sicura e piacevole.  Adobe AIR consente alle aziende di integrare facilmente i contenuti multimediali per creare un&#39;esperienza utente interattiva e coinvolgente. Consente agli sviluppatori di utilizzare strumenti familiari come HTML, JavaScript, Flash o  software Flex® Adobe® per distribuire la combinazione unica di applicazioni Internet avanzate a Windows, Macintosh o Linux.

Le aziende hanno il controllo completo dell&#39;interfaccia utente e possono progettare un&#39;esperienza utente che rifletta e rafforzi il proprio marchio. Grazie al supporto integrato per la riproduzione di contenuto protetto con  Adobe Access SDK,  Adobe AIR consente di creare catene di distribuzione di contenuti end-to-end personalizzate.

Per maggiori informazioni su  Adobe AIR, visita: [www.adobe.com/go/air](https://www.adobe.com/go/air)

## Applicazioni iOS e Android native {#native-ios-and-android-applications}

Applicazioni iOS e Android native Disponibile solo per  clienti Adobe Primetime,  accesso Adobe DRM 4.0 e versioni successive può essere utilizzato per proteggere i video utilizzati nelle applicazioni native (non Flash) su dispositivi mobili. Affinché un&#39;applicazione utilizzi questo contenuto protetto, è necessario implementarlo utilizzando le librerie client Adobe Primetime .

Per maggiori informazioni su  Adobe Primetime, visita: [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)