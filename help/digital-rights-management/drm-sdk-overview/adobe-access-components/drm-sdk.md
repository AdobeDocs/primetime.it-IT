---
description: I componenti principali di Primetime DRM sono costituiti da un SDK Java e dagli ambienti di runtime client Flash Player e Adobe AIR.
title: Client SDK Java, Flash Player e Adobe AIR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---


# SDK Adobe Primetime DRM {#section_522E57DFEEFF4794978FF2D366B83690}

Primetime DRM viene fornito come SDK Java che fornisce i blocchi predefiniti da cui puoi creare un&#39;implementazione del server. Utilizzando l&#39;SDK puoi creare una soluzione DRM Primetime adatta al modello di business della tua organizzazione.

Le API Java fornite nell’SDK sono descritte nelle seguenti sottosezioni.

## API Java per la gestione dei domini dei gruppi di dispositivi{#java-apis-for-managing-device-group-domains}

Queste API vengono utilizzate per consentire al server di gestire le richieste client per l’unione e l’uscita dai domini del gruppo di dispositivi.

Un dominio di gruppo di dispositivi è una raccolta logica di dispositivi in grado di condividere licenze tra loro. Affinché ciò accada, ogni dispositivo deve prima iscriversi/registrarsi allo stesso dominio. L’SDK DRM di Primetime, in esecuzione su un server, deve gestire le richieste di join (register) del dominio dispositivo e le richieste di congedo dal dominio del dispositivo (de-register). Ai dispositivi che non fanno parte di alcun dominio verranno rilasciate licenze associate a tale dispositivo, che non possono essere condivise con nessun altro dispositivo.

## API Java per la protezione dei contenuti{#java-apis-for-protecting-content}

Queste API vengono utilizzate per definire i diritti e preparare i contenuti per la distribuzione. Le API di protezione dei contenuti sono:

* Gestione dei criteri

   L’API di gestione dei criteri viene utilizzata per creare e modificare i criteri da applicare ai contenuti. I criteri possono essere creati o aggiornati, comprese le informazioni su come ottenere/impostare tutte le regole di utilizzo e consentire l’utilizzo di parametri aggiuntivi in uno spazio dei nomi personalizzato.

* Pacchetto di contenuti

   L’API per la creazione di pacchetti di contenuti viene utilizzata per crittografare i contenuti e recuperare i metadati dal contenuto in pacchetto.

## API Java per il rilascio di licenze{#java-apis-for-issuing-licenses}

Queste API vengono utilizzate quando un client richiede una licenza dal server. L&#39;SDK supporta le seguenti richieste dal client:

* Autenticazione

   L’API di autenticazione può essere utilizzata per gestire le richieste di autenticazione e generare token di autenticazione.

* Generazione e acquisizione di licenze

   L’API di generazione e acquisizione della licenza viene utilizzata per generare una licenza per l’utente.

* Supporto per client e contenuti Adobe AIR versione 1.5

   Ai fini della compatibilità con le versioni precedenti, l’SDK dispone di API per gestire le richieste di applicazioni AIR create per l’utilizzo con AIR versione 1.5 e precedenti e contenuti protetti.

## Implementazione di riferimento {#reference-implementation}

L&#39;SDK include un&#39;implementazione di riferimento, una semplice implementazione DRM di Adobe Primetime che dimostra come utilizzare le API Java. L’implementazione di riferimento fornisce un server licenze, un pacchetto cartelle controllate, un’applicazione AIR Primetime DRM Manager e strumenti a riga di comando per la creazione di pacchetti di contenuti e la gestione dei criteri in base alle API Java. Per ulteriori informazioni sull’implementazione di riferimento DRM di Primetime, consulta Protezione dei contenuti .