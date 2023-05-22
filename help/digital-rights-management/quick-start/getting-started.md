---
title: Guida introduttiva
description: Guida introduttiva
copied-description: true
exl-id: d29d141e-913c-4b9d-979c-91c486414071
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Guida introduttiva {#getting-started}

In questo documento vengono descritti i passaggi necessari per configurare e distribuire rapidamente un ecosistema Adobe Primetime DRM che utilizza il download progressivo per la distribuzione dei contenuti e il server DRM Primetime per lo streaming protetto per la distribuzione delle licenze. Ulteriori dettagli su ciascun passaggio sono forniti nelle seguenti guide:

* *Utilizzo del server DRM Primetime per la protezione dei contenuti*
* *Utilizzo del server DRM Primetime per lo streaming protetto*

Il server DRM di Primetime per lo streaming protetto è un server dalle funzionalità minime che non include codice sorgente. Per un server modificabile con origine Java completa, vedi *Utilizzo delle implementazioni di riferimento DRM di Primetime* guida. Se imposti un server di licenze di riferimento, questo sostituirà il *Configurazione e distribuzione di Primetime DRM Server per lo streaming protetto (server licenze)* passaggio.

## Prerequisiti {#prerequisites}

Prima di iniziare, completa le seguenti attività:

* Ottenere due computer Windows o Linux:

   * Un computer sarà il server licenze.
   * Un computer sarà Content Server.

* Installare le applicazioni seguenti in entrambi i computer:

   * Tomcat 6.0.18
   * Java 1.6

## Ottenere i certificati {#obtain-certificates}

Una volta consegnato il software SDK, l’amministratore del certificato dell’azienda designato riceverà un invito a completare il processo di registrazione del certificato Adobe Primetime DRM. Per ulteriori informazioni, vedere *Guida alla registrazione dei certificati DRM di Primetime*.

1. L’Amministratore nomina almeno una persona come richiedente del certificato.
1. Il Richiedente certificato genera una chiave privata e una CSR.
1. Il richiedente invia una richiesta di certificato.
1. L’amministratore della società approva la richiesta.
1. L’amministratore del certificato di Adobe conferma l’invio.
1. Il richiedente riceve il certificato, lo associa alla chiave privata e lo distribuisce. come descritto in .

   Per ulteriori informazioni sulla distribuzione del certificato, vedi *Distribuzione del server Adobe Primetime DRM per lo streaming protetto* guida.
1. I passaggi da 3 a 6 devono essere completati per ciascun tipo di certificato.

   Per la versione di produzione DRM di Primetime, il richiedente deve effettuare richieste separate per i certificati server licenze, di imballaggio e di trasporto, che sono validi per due anni.

   I clienti che utilizzano le versioni di valutazione DRM di Primetime o di prova necessitano di un solo certificato valido rispettivamente per 1 anno/90 giorni.
