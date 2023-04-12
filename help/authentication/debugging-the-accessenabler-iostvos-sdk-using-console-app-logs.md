---
title: Debug dell’SDK iOS/tvOS di AccessEnabler tramite i registri delle app della console
description: Debug dell’SDK iOS/tvOS di AccessEnabler tramite i registri delle app della console
source-git-commit: 326f97d058646795cab5d062fa5b980235f7da37
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---


# Debug dell’SDK iOS/tvOS di AccessEnabler tramite i registri delle app della console {#debugging-the-accessenabler-iostvos-sdk-using-console-app-logs}

>[!NOTE]
>
>Il contenuto di questa pagina viene fornito solo a scopo informativo. L’utilizzo di questa API richiede una licenza corrente a partire da Adobe. Non è consentito alcun uso non autorizzato.


## Panoramica

Lo scopo di questo documento è quello di acquisire e presentare l&#39;evoluzione del meccanismo di registrazione dell&#39;SDK iOS/tvOS di AccessEnabler insieme ad alcuni dettagli utili per il debug del framework AccessEnabler tramite i registri delle app Console.

## Stato del meccanismo di registrazione

Lo scopo del meccanismo di registrazione di AccessEnabler iOS/tvOS è quello di emettere messaggi utili per la risoluzione dei problemi che un&#39;applicazione che utilizza il framework AccessEnabler potrebbe incontrare a causa di esso.

### AccessEnabler iOS/tvOS 3.5.0 e versioni successive

A partire dalla versione iOS/tvOS 3.5.0 di AccessEnabler, il meccanismo di registrazione introduce i seguenti miglioramenti man mano che cambiano:

* Il framework AccessEnabler utilizza Apple consigliato [OSLog](https://developer.apple.com/documentation/os/oslog) implementazione.

* Il framework AccessEnabler introduce la possibilità di filtrare i registri delle app Console in base al sottosistema: **com.adobe.pass.AccessEnabler**. Tutti i messaggi inviati dall&#39;SDK fanno parte di com.adobe.pass.AccessEnabler.

* Il framework AccessEnabler introduce la possibilità di filtrare i registri delle app Console in base a Qualsiasi (prefisso): **[AccessEnabler]**. Tutti i messaggi inviati dall’SDK hanno il prefisso [AccessEnabler].

* Il framework AccessEnabler introduce la possibilità di filtrare i registri delle app Console in base alla categoria: **debug**, **errore** in combinazione con uno dei due criteri sopra indicati: Sottosistema o Qualsiasi (prefisso).

## Debug tramite i registri delle app della console

A seconda dei problemi esaminati, è possibile includere o escludere i messaggi di log emessi dal framework AccessEnabler. Di seguito sono riportati alcuni dettagli utili che possono esserti utili durante le indagini e durante l’utilizzo dei log delle app Console.


### AccessEnabler iOS/tvOS 3.5.0 e versioni successive

#### Incluso {#including}

Prima di tutto, per poter vedere i messaggi di registrazione inviati dal framework AccessEnabler, **deve** seleziona &quot;Includi messaggi di informazioni&quot; e &quot;Includi messaggi di debug&quot; nella sezione Azione dell’app Console, come illustrato nell’immagine seguente.

![](assets/include-info-debug-msg.png)


Per poter eseguire il debug della funzionalità dell&#39;SDK iOS/tvOS di AccessEnabler e **vedere** i registri del framework di AccessEnabler consentono di:

* Ricerca nell’app Console tramite **Sottosistema** che equivale al valore com.adobe.pass.AccessEnabler come nell&#39;immagine seguente.

![](assets/subsys-console-app.png)

* Ricerca nell’app Console tramite **Qualsiasi** che contiene l’opzione
   [AccessEnabler] come nell&#39;immagine seguente.

![](assets/any-optn-console-app.png)

Accanto ai due criteri di cui sopra è anche possibile utilizzare il **Categoria** in combinazione con **Sottosistema** o **Any (prefisso)** per cercare esplicitamente **debug** o **errore** messaggi di livello emessi dall&#39;SDK iOS/tvOS di AccessEnabler.

#### Esclusione

Per poter eseguire meglio il debug della funzionalità di altri componenti e **escludere** i registri del framework di AccessEnabler consentono di:

* Ricerca nell’app Console tramite **Sottosistema** che non è uguale al valore com.adobe.pass.AccessEnabler.
* Ricerca nell’app Console tramite **Qualsiasi** che non contiene [AccessEnabler] valore.

## Segnalazione di un problema

Quando segnali un problema all’autenticazione di Adobe Primetime, prendi in considerazione i seguenti suggerimenti:

* provare a fornire i passaggi di riproduzione.
* cerca di fornire le versioni del sistema operativo e i modelli di dispositivo su cui si verifica il problema.
* prova a fornire la versione dell’SDK iOS/tvOS di AccessEnabler che si trova in presenza del problema.
* cerca di acquisire e allegare tutti i messaggi di registrazione dell&#39;SDK di AccessEnabler iOS/tvOS utilizzando una delle due opzioni presentate in [Incluso](#including) sezione .
