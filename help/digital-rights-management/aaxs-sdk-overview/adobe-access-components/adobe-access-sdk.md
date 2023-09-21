---
description: I componenti principali di Adobe Access sono costituiti da un SDK Java e dagli ambienti di runtime client Flash Player e Adobe AIR.
title: Java SDK, Flash Player e client Adobe AIR
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# Componenti di accesso Adobe{#adobe-access-components}

I componenti principali di Adobe Access sono costituiti da un SDK Java e dagli ambienti di runtime client Flash Player e Adobe AIR.

Per ulteriori informazioni sulla configurazione dell’SDK, consulta Configurazione dell’SDK in *Utilizzo dell’SDK di accesso di Adobe per proteggere il contenuto.*

L’SDK di accesso Adobe consente di sviluppare una soluzione di gestione dei diritti digitali che si integra con l’infrastruttura aziendale esistente della tua organizzazione, ad esempio i sistemi di gestione dei contenuti, fatturazione e controllo degli accessi utente. Flash Player e Adobe AIR consentono di creare e distribuire facilmente applicazioni tramite le quali i consumatori possono accedere e visualizzare grandi librerie di contenuti digitali.

## SDK di accesso agli Adobi {#section_6AA3DC7BAE354472AE179BBC9AF6BD27}

Adobe Access viene fornito come SDK Java che fornisce i blocchi predefiniti da cui è possibile creare un’implementazione del server. Utilizzando l’SDK puoi creare una soluzione di accesso Adobe adatta al modello di business della tua organizzazione.

Le API Java fornite nell’SDK sono descritte nelle seguenti sottosezioni.

## API Java per la gestione dei domini dei gruppi di dispositivi {#java-apis-for-managing-device-group-domains}

Queste API vengono utilizzate per consentire al server di gestire le richieste dei client per l’unione e l’uscita dai domini del gruppo di dispositivi.

Un dominio del gruppo di dispositivi è una raccolta logica di dispositivi in grado di condividere le licenze tra loro. Affinché ciò accada, ogni dispositivo deve prima aderire/registrarsi allo stesso dominio. L’SDK per l’accesso degli Adobi, in esecuzione su un server, deve gestire le richieste di unione (registrazione) del dominio dispositivo e le richieste di uscita (annullamento della registrazione) del dominio dispositivo. Ai dispositivi che non fanno parte di alcun dominio verranno rilasciate licenze associate a tale dispositivo, che non possono essere condivise con altri dispositivi.

## API Java per la protezione dei contenuti {#java-apis-for-protecting-content}

Queste API vengono utilizzate per definire i diritti e preparare i contenuti per la distribuzione. Le API di protezione dei contenuti sono:

* Gestione delle policy

  L’API di gestione dei criteri viene utilizzata per creare e modificare i criteri da applicare al contenuto. È possibile creare o aggiornare i criteri, incluso ottenere/impostare tutte le regole di utilizzo e consentire parametri aggiuntivi in uno spazio dei nomi personalizzato.

* Confezionamento dei contenuti

  L’API per la creazione di pacchetti di contenuti viene utilizzata per crittografare i contenuti e recuperare i metadati dai contenuti inclusi nel pacchetto.

## API Java per il rilascio di licenze {#java-apis-for-issuing-licenses}

Queste API vengono utilizzate quando un client richiede una licenza dal server. L’SDK supporta le seguenti richieste del client:

* Autenticazione

  L’API di autenticazione può essere utilizzata per gestire le richieste di autenticazione e generare token di autenticazione.

* Generazione e acquisizione di licenze

  L’API di generazione e acquisizione delle licenze viene utilizzata per generare una licenza per l’utente.

* Supporto per client e contenuti Adobe AIR versione 1.5

  Ai fini della compatibilità con le versioni precedenti, l’SDK dispone di API per gestire le richieste provenienti da applicazioni AIR create per l’utilizzo con AIR versione 1.5 e precedenti client e contenuti protetti.

## Implementazione di riferimento {#reference-implementation}

L’SDK include un’implementazione di riferimento, una semplice distribuzione di accesso di Adobe che illustra come utilizzare le API Java. L’implementazione di riferimento fornisce un server licenze, uno strumento di creazione pacchetti cartelle controllate, un’applicazione AIR per Adobe Access Manager e strumenti per riga di comando per la creazione di pacchetti di contenuti e la gestione delle policy basati sulle API Java. Per ulteriori informazioni sull’implementazione di riferimento per gli accessi agli Adobi, consulta *Protezione dei contenuti*.

## Adobe Access Server per Streaming protetto {#adobe-access-server-for-protected-streaming}

Nei casi di utilizzo dello streaming in cui il contenuto è protetto con l&#39;accesso Adobe, ad Adobe HTTP Dynamic Streaming, il software include anche Adobe Access Server for Protected Streaming. Questa soluzione può essere facilmente implementata su un contenitore servlet come Tomcat e può raggiungere un elevato livello di scalabilità e prestazioni per soddisfare le più grandi esigenze di distribuzione dei contenuti.

## Flash Player Adobe {#adobe-flash-player}

Flash Player è un plug-in e runtime del browser leggero che offre esperienze utente coerenti e coinvolgenti, riproduzione audio/video straordinaria e portata pervasiva. Il Flash Player fornisce una riproduzione di alta qualità di contenuti video in streaming o scaricati. Per gli editori di contenuti, Flash Player fornisce i mezzi per personalizzare le schermate di riproduzione che circondano i contenuti, consentendo esperienze di branding più approfondite e la monetizzazione attraverso la pubblicità utilizzando banner e sovrapposizioni. Per i consumatori, il Flash Player presenta un modo intuitivo e visivamente accattivante per visualizzare i contenuti video.

Per ulteriori informazioni sul Flash Player, visitare il sito: [www.adobe.com/go/flashplayer](https://www.adobe.com/go/flashplayer)

## Adobe AIR {#adobe-air}

Adobe AIR è un runtime cross-operation system che consente ai produttori di contenuti di estendere al desktop gli investimenti esistenti sul web progettando applicazioni multimediali personalizzate. Basata su tecnologie aperte e comprovate, rappresenta un modo affidabile e semplificato per le aziende di sviluppare e implementare applicazioni personalizzate affidabili per offrire un&#39;esperienza utente più sicura e piacevole. Adobe AIR consente alle aziende di integrare facilmente i rich media per creare un’esperienza utente più coinvolgente e interattiva. Consente agli sviluppatori di utilizzare strumenti familiari come HTML, JavaScript, Flex® o Adobe® Flash per distribuire la combinazione unica di applicazioni Internet avanzate su Windows, Macintosh o Linux.

Le aziende hanno il controllo completo dell&#39;interfaccia utente e possono progettare un&#39;esperienza utente per riflettere e rafforzare il proprio marchio. Grazie al supporto integrato per la riproduzione di contenuti protetti con l’SDK Adobe Access, Adobe AIR consente di creare catene di distribuzione dei contenuti personalizzate e complete.

## Applicazioni native iOS e Android {#native-ios-and-android-applications}

Applicazioni native per iOS e Android Disponibile solo per i clienti Adobe Primetime, è possibile utilizzare Adobe Access DRM 4.0 e versioni successive per proteggere i video utilizzati nelle applicazioni native (non di Flash) sui dispositivi mobili. Affinché un’applicazione possa utilizzare questo contenuto protetto, è necessario implementarlo utilizzando le librerie client di Adobe Primetime.

Per ulteriori informazioni su Adobe Primetime, visita: [https://www.adobe.com/solutions/primetime.html](https://www.adobe.com/solutions/primetime.html)
