---
description: I componenti principali di Primetime DRM sono un SDK Java e gli ambienti di runtime client Flash Player e Adobe AIR.
title: Java SDK, Flash Player e client Adobe AIR
exl-id: 5422d282-da9c-4810-a782-3c3af5fdeb3f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# SDK ADOBE PRIMETIME DRM {#section_522E57DFEEFF4794978FF2D366B83690}

DRM di Primetime viene fornito come SDK Java che fornisce i blocchi predefiniti da cui è possibile creare un’implementazione del server. Utilizzando l’SDK puoi creare una soluzione DRM Primetime adatta al modello di business della tua organizzazione.

Le API Java fornite nell’SDK sono descritte nelle seguenti sottosezioni.

## API Java per la gestione dei domini dei gruppi di dispositivi{#java-apis-for-managing-device-group-domains}

Queste API vengono utilizzate per consentire al server di gestire le richieste dei client per l’unione e l’uscita dai domini del gruppo di dispositivi.

Un dominio del gruppo di dispositivi è una raccolta logica di dispositivi in grado di condividere le licenze tra loro. Affinché ciò accada, ogni dispositivo deve prima aderire/registrarsi allo stesso dominio. L’SDK di Primetime DRM, in esecuzione su un server, deve gestire le richieste di unione (registrazione) del dominio dispositivo e le richieste di uscita (cancellazione) dal dominio dispositivo. Ai dispositivi che non fanno parte di alcun dominio verranno rilasciate licenze associate a tale dispositivo, che non possono essere condivise con altri dispositivi.

## API Java per la protezione dei contenuti{#java-apis-for-protecting-content}

Queste API vengono utilizzate per definire i diritti e preparare i contenuti per la distribuzione. Le API di protezione dei contenuti sono:

* Gestione delle policy

   L’API di gestione dei criteri viene utilizzata per creare e modificare i criteri da applicare al contenuto. È possibile creare o aggiornare i criteri, incluso ottenere/impostare tutte le regole di utilizzo e consentire parametri aggiuntivi in uno spazio dei nomi personalizzato.

* Confezionamento dei contenuti

   L’API per la creazione di pacchetti di contenuti viene utilizzata per crittografare i contenuti e recuperare i metadati dai contenuti inclusi nel pacchetto.

## API Java per il rilascio di licenze{#java-apis-for-issuing-licenses}

Queste API vengono utilizzate quando un client richiede una licenza dal server. L’SDK supporta le seguenti richieste del client:

* Autenticazione

   L’API di autenticazione può essere utilizzata per gestire le richieste di autenticazione e generare token di autenticazione.

* Generazione e acquisizione di licenze

   L’API di generazione e acquisizione delle licenze viene utilizzata per generare una licenza per l’utente.

* Supporto per client e contenuti Adobe AIR versione 1.5

   Ai fini della compatibilità con le versioni precedenti, l’SDK dispone di API per gestire le richieste provenienti da applicazioni AIR create per l’utilizzo con AIR versione 1.5 e precedenti client e contenuti protetti.

## Implementazione di riferimento {#reference-implementation}

L’SDK include un’implementazione di riferimento, una semplice distribuzione Adobe Primetime DRM che illustra come utilizzare le API Java. L’implementazione di riferimento fornisce un server licenze, uno strumento di creazione pacchetti cartelle controllate, un’applicazione AIR di Primetime DRM Manager e strumenti per riga di comando per la creazione di pacchetti di contenuti e la gestione delle policy basati sulle API Java. Per ulteriori informazioni sull’implementazione di riferimento di Primetime DRM, consulta Protezione dei contenuti.
