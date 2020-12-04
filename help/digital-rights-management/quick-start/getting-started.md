---
seo-title: Guida introduttiva
title: Guida introduttiva
uuid: 2002cf94-c8a7-4820-a560-6d9f7f33ee97
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Guida introduttiva {#getting-started}

Questo documento fornisce i passaggi per una rapida configurazione e implementazione di un ecosistema DRM  Adobe Primetime che utilizza il download progressivo per distribuire il contenuto, e il server DRM Primetime per lo streaming protetto per la distribuzione delle licenze. Ulteriori dettagli su ciascun passaggio sono forniti nelle seguenti guide:

* *Utilizzo del server DRM Primetime per la protezione dei contenuti*
* *Utilizzo del server DRM Primetime per lo streaming protetto*

Il server DRM di Primetime per lo streaming protetto è un server con funzionalità minima che non include il codice sorgente. Per un server modificabile con origine Java completa, consultate la guida *Using the Primetime DRM Reference Implementation* (Utilizzo delle implementazioni di riferimento DRM di Primetime). Se si configura un server Licenze di riferimento, che sostituisce il passaggio *Setup (Impostazione) e implementa Primetime DRM Server for Protected Streaming (License Server)*.

## Prerequisiti {#prerequisites}

Prima di iniziare, effettuate le seguenti operazioni:

* Ottenere due computer Windows o Linux:

   * Un computer sarà il server licenze.
   * Un computer sarà Content Server.

* Installate le seguenti applicazioni su entrambi i computer:

   * Tomcat 6.0.18
   * Java 1.6

## Ottieni certificati {#obtain-certificates}

Dopo la distribuzione del software SDK, l&#39;amministratore di certificati aziendali designato riceverà un invito a completare il processo di registrazione  certificati DRM di Adobe Primetime. Per ulteriori informazioni, vedere la *Guida all&#39;iscrizione ai certificati DRM di Primetime*.

1. L&#39;amministratore nomina almeno una persona come richiedente del certificato.
1. Il richiedente del certificato genera una chiave privata e un CSR.
1. Il richiedente invia una richiesta di certificato.
1. L&#39;amministratore della società approva la richiesta.
1. L&#39;amministratore  certificati di Adobe conferma l&#39;invio.
1. Il richiedente riceve il certificato, lo vincola con la chiave privata e distribuisce il certificato. come descritto in .

   Per ulteriori informazioni sulla distribuzione del certificato, vedere la guida *Implementazione del server DRM  Adobe Primetime per lo streaming protetto*.
1. I passaggi da 3 a 6 devono essere completati per ciascun tipo di certificato.

   Per la versione di produzione DRM di Primetime, il richiedente deve effettuare richieste separate per i certificati License Server, Packaging e Transport, validi per due anni.

   I clienti che utilizzano le versioni di valutazione o di prova DRM di Primetime hanno bisogno di un solo certificato valido rispettivamente per 1 anno/90 giorni.