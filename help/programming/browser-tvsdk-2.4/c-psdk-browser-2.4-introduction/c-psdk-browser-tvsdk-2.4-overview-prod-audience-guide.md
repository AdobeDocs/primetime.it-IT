---
description: Questa guida fornisce informazioni su come sviluppare applicazioni di lettore video utilizzando il browser TVSDK.
title: Panoramica del prodotto e pubblico
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Panoramica del prodotto e pubblico{#product-overview-and-audience}

Questa guida fornisce informazioni su come sviluppare applicazioni di lettore video utilizzando il browser TVSDK.

## Panoramica del prodotto {#section_1C66E736CEFD4246B7C7C99AADD48118}

Adobe Primetime Software Development Kit (Browser TVSDK) è un toolkit che consente di aggiungere funzionalità avanzate di riproduzione video, protezione dei contenuti e pubblicità alle applicazioni di lettore video basate su browser. Il browser TVSDK fornisce API JavaScript per la creazione di applicazioni video basate su browser e include il supporto per la riproduzione nelle seguenti modalità:

* Solo HTML5
* HTML5 con fallback flash automatico
* Flash sempre

Questa versione include le API TVSDK per browser e un esempio di implementazione di riferimento.

### Framework interfaccia utente

Per accelerare lo sviluppo dell’interfaccia utente per le applicazioni di lettore video basate su JavaScript per i browser, il browser TVSDK include un framework di interfaccia utente composto da API per:

* Includi controlli predefiniti dell’interfaccia utente quali riproduzione/pausa, volume e così via
* Facile aggiunta (o rimozione) di controlli avanzati dell&#39;interfaccia utente per la riproduzione senza manipolare direttamente la struttura DOM
* Facile configurazione del comportamento per i controlli dell’interfaccia utente associati
* Creare controlli personalizzati dell’interfaccia utente
* Interfaccia utente del lettore in base ai requisiti

Per ulteriori informazioni sulle API per il framework dell&#39;interfaccia utente, consulta [Framework di interfaccia utente per il browser TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/index.html).

## Pubblico {#section_DFC9DECC2E30426DBBDDEA4E288E666C}

Questa guida presuppone che tu comprenda come sviluppare applicazioni e lettori video utilizzando JavaScript. È possibile implementare un lettore video e incorporare le funzioni del browser TVSDK.