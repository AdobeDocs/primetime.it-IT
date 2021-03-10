---
title: Introduzione
description: Introduzione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Guida introduttiva {#getting-started}

Questo documento fornisce i passaggi per una rapida configurazione e distribuzione di un ecosistema DRM di Adobe Primetime che utilizza il download progressivo per distribuire i contenuti e il server DRM di Primetime per lo streaming protetto per la distribuzione delle licenze. Ulteriori dettagli su ogni passaggio sono forniti nelle seguenti guide:

* *Utilizzo del server DRM di Primetime per la protezione dei contenuti*
* *Utilizzo del server DRM di Primetime per lo streaming protetto*

Il server DRM di Primetime per lo streaming protetto è un server a funzionalità minima che non include il codice sorgente. Per un server modificabile con origine Java completa, consulta la guida *Using the Primetime DRM Reference Implementations* . Se si imposta un server Licenze di riferimento, questo sostituisce il passaggio *Configurazione e distribuzione di Primetime DRM Server for Protected Streaming (License Server)* .

## Prerequisiti {#prerequisites}

Prima di iniziare, completa le seguenti attività:

* Ottenere due computer Windows o Linux:

   * Un computer sarà il server licenze.
   * Un computer sarà Content Server.

* Installa le seguenti applicazioni su entrambi i computer:

   * Tomcat 6.0.18
   * Java 1.6

## Recuperare i certificati {#obtain-certificates}

Dopo la consegna del software SDK, l’amministratore del certificato aziendale designato riceverà un invito a completare il processo di registrazione del certificato DRM di Adobe Primetime. Per ulteriori informazioni, consulta la *Guida all’iscrizione al certificato DRM di Primetime*.

1. L’amministratore nomina almeno una persona come Richiedente certificato.
1. Il richiedente del certificato genera una chiave privata e una CSR.
1. Il richiedente invia una richiesta di certificato.
1. L&#39;amministratore della società approva la richiesta.
1. L’amministratore del certificato di Adobe conferma l’invio.
1. Il richiedente riceve il certificato, lo associa alla chiave privata e distribuisce il certificato. come descritto in .

   Per ulteriori informazioni sulla distribuzione del certificato, consulta la guida *Implementazione del server DRM Adobe Primetime per lo streaming protetto* .
1. I passaggi da 3 a 6 devono essere completati per ciascun tipo di certificato.

   Per la versione di produzione DRM di Primetime, il richiedente deve effettuare richieste separate per i certificati License Server, Packaging e Transport, validi per due anni.

   I clienti che utilizzano le versioni di valutazione DRM di Primetime o di prova necessitano solo di un certificato valido rispettivamente per 1 anno / 90 giorni.