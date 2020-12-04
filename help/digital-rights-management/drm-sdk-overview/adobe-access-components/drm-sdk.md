---
description: I componenti principali di Primetime DRM sono costituiti da un SDK Java e dagli ambienti runtime client Adobe AIR Flash Player e .
seo-description: I componenti principali di Primetime DRM sono costituiti da un SDK Java e dagli ambienti runtime client Adobe AIR Flash Player e .
seo-title: 'Java SDK, Flash Player e client Adobe AIR '
title: 'Java SDK, Flash Player e client Adobe AIR '
uuid: e6daed27-3803-4ef7-ba25-4a180af7502f
translation-type: tm+mt
source-git-commit: 635e2893439c5459907c54d2c3bd86f58da0eec5
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


#  Adobe Primetime DRM SDK {#section_522E57DFEEFF4794978FF2D366B83690}

Primetime DRM viene distribuito come SDK Java che fornisce i blocchi costitutivi dai quali è possibile creare un&#39;implementazione del server. Con l’SDK puoi creare una soluzione DRM Primetime adatta al modello aziendale dell’organizzazione.

Le API Java fornite nell’SDK sono descritte nelle seguenti sottosezioni.

## API Java per la gestione dei domini dei gruppi di dispositivi{#java-apis-for-managing-device-group-domains}

Queste API vengono utilizzate per consentire al server di gestire le richieste client per l&#39;adesione e l&#39;uscita dai domini dei gruppi di dispositivi.

Un dominio di gruppo di dispositivi è una raccolta logica di dispositivi in grado di condividere le licenze tra loro. Affinché ciò possa avvenire, ogni dispositivo deve prima registrarsi o registrarsi nello stesso dominio. L&#39;SDK DRM di Primetime, in esecuzione su un server, deve gestire le richieste di partecipazione (registro) del dominio dispositivo e le richieste di congedo (deregistrazione) del dominio dispositivo. Ai dispositivi che non fanno parte di un dominio verranno rilasciate licenze associate a tale dispositivo, che non possono essere condivise con altri dispositivi.

## API Java per la protezione del contenuto{#java-apis-for-protecting-content}

Queste API vengono utilizzate per definire i diritti e preparare il contenuto per la distribuzione. Le API per la protezione del contenuto sono:

* Gestione dei criteri

   L&#39;API di gestione criteri viene utilizzata per creare e modificare i criteri da applicare al contenuto. I criteri possono essere creati o aggiornati, incluso ottenere/impostare tutte le regole di utilizzo e consentire parametri aggiuntivi in uno spazio dei nomi personalizzato.

* Creazione di contenuti

   L&#39;API per la creazione di pacchetti di contenuto viene utilizzata per cifrare il contenuto e recuperare i metadati dal contenuto incluso nel pacchetto.

## API Java per il rilascio di licenze{#java-apis-for-issuing-licenses}

Queste API vengono utilizzate quando un client richiede una licenza dal server. L’SDK supporta le seguenti richieste dal client:

* Autenticazione

   L&#39;API di autenticazione può essere utilizzata per gestire le richieste di autenticazione e generare token di autenticazione.

* Generazione e acquisizione di licenze

   L&#39;API di generazione e acquisizione della licenza viene utilizzata per generare una licenza per l&#39;utente.

* Supporto per  client e contenuti Adobe AIR versione 1.5

   Ai fini della compatibilità con le versioni precedenti, l’SDK dispone di API per gestire le richieste delle applicazioni AIR create per l’uso con i client AIR versione 1.5 e versioni precedenti e il contenuto protetto.

## Implementazione di riferimento {#reference-implementation}

L&#39;SDK include un&#39;implementazione di riferimento, una semplice implementazione DRM  Adobe Primetime che illustra come utilizzare le API Java. L&#39;implementazione di riferimento fornisce un server licenze, un pacchetto cartelle esaminate, un&#39;applicazione AIR DRM Manager Primetime e strumenti della riga di comando per la creazione di pacchetti di contenuto e la gestione dei criteri basati sulle API Java. Per ulteriori informazioni sull&#39;implementazione di riferimento DRM di Primetime, consulta Protezione dei contenuti.