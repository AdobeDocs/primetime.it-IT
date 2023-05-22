---
description: Per usare il browser TVSDK, devi creare e configurare un lettore di base. Per la riproduzione di contenuti video, puoi creare un lettore di base in due modi, utilizzando il browser TVSDK o il framework dell’interfaccia utente.
title: Lettore di base
exl-id: f51d7bf7-1784-447e-97ab-275ea53d5e46
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Panoramica {#basic-player-overview}

Per usare il browser TVSDK, devi creare e configurare un lettore di base. Per la riproduzione di contenuti video, puoi creare un lettore di base in due modi: utilizzando il browser TVSDK o il framework dell’interfaccia utente.

## Utilizzo del TVSDK del browser {#section_4D1C6D4B3A3447DFA2AA0229E140E2D9}

Utilizza le API fornite con il browser TVSDK direttamente per codificare il lettore video. L’SDK offre framework, utility e un lettore di riferimento da cui lavorare.

>[!TIP]
>
>Per visualizzare questo funzionamento in un lettore di riferimento, non specificare attributi con `videoDiv`.

## Utilizzo del framework dell’interfaccia utente {#section_AE02384CFEF64A448C108232AB62A9FF}

Questo modulo viene utilizzato per creare istanze del lettore, in cui ogni istanza è associata a un elemento DOM (Document Object Model) fornito dal chiamante. Oltre a disporre di un’istanza del Browser TVSDK, ogni istanza del lettore ospita una serie di controlli che costituiscono l’interfaccia utente del lettore.

L&#39;attuazione di ciascun controllo consiste in due aspetti:

* Un `HTMLElement`, che è la rappresentazione visiva del componente sullo schermo
* A `Behavior`, che gestisce `HTMLElement` e fornisce un’API per le interazioni

I dettagli su questi controlli vengono forniti al `VideoPlayer` utilizzando un oggetto config, che viene passato al lettore al momento della creazione dell’istanza. Per impostazione predefinita, ogni componente forma una gerarchia di oggetti, con l’elemento fornito all’istanza del lettore nella radice della struttura. Ogni componente viene creato e aggiunto al DOM nella posizione appropriata.

Ogni componente ha un nome, che corrisponde alla sua chiave nell&#39;oggetto di configurazione quando l&#39;oggetto viene registrato. La classe CSS dell’elemento DOM sottostante è formata da `vp-` prefisso aggiunto al nome del componente.

I componenti possono essere estesi o sostituiti, la loro configurazione può essere modificata e le proprietà iniziali impostate. Ciò ti consente di avere un controllo più ampio sulle proprietà API, sul nome della classe CSS e, facoltativamente, su alcuni aspetti dell’implementazione del componente. Queste opzioni possono essere utilizzate per personalizzare la funzionalità e consentire più istanze di un componente che possono essere formattate o configurate singolarmente.

È possibile accedere a tutte le istanze dei componenti con `.behaviors` proprietà. Le istanze possono essere attivate e disattivate e visualizzate o nascoste. Tuttavia, una volta create le istanze, queste non possono essere rimosse.
