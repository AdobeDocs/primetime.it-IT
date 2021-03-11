---
description: Per utilizzare l'SDK del browser, è necessario creare e configurare un lettore di base. Per la riproduzione di contenuti video, è possibile creare un lettore di base in due modi utilizzando il browser TVSDK o il framework dell'interfaccia utente.
title: Lettore base
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Panoramica {#basic-player-overview}

Per utilizzare l&#39;SDK del browser, è necessario creare e configurare un lettore di base. Per la riproduzione di contenuti video, è possibile creare un lettore di base in uno dei due modi seguenti: utilizzare il browser TVSDK o il framework dell&#39;interfaccia utente.

## Utilizzo del browser TVSDK {#section_4D1C6D4B3A3447DFA2AA0229E140E2D9}

Utilizza le API fornite con il browser TVSDK direttamente per codificare il lettore video. L&#39;SDK fornisce framework e utility, nonché un lettore di riferimento da cui lavorare.

>[!TIP]
>
>Per vedere come funziona in un lettore di riferimento, non specificare alcun attributo con `videoDiv`.

## Utilizzo del framework dell&#39;interfaccia utente {#section_AE02384CFEF64A448C108232AB62A9FF}

Questo modulo viene utilizzato per creare istanze del lettore, in cui ogni istanza è associata a un elemento DOM (Document Object Model) fornito dal chiamante. Oltre ad avere un&#39;istanza del browser TVSDK, ogni istanza del lettore ospita una serie di controlli che compongono l&#39;interfaccia utente per il lettore.

L&#39;attuazione di ciascun controllo consiste in due aspetti:

* Una `HTMLElement`, che è la rappresentazione visiva del componente sullo schermo
* A `Behavior`, che gestisce `HTMLElement` e fornisce un’API per le interazioni

I dettagli su questi controlli vengono forniti al `VideoPlayer` utilizzando un oggetto config, che viene passato al lettore alla relativa creazione di istanza. Per impostazione predefinita, ogni componente forma una gerarchia di oggetti, con l’elemento fornito all’istanza del lettore nella parte principale della struttura. Man mano che ciascun componente viene creato, viene aggiunto al DOM nella posizione appropriata.

Ogni componente ha un nome, corrispondente alla sua chiave nell&#39;oggetto config quando l&#39;oggetto è registrato. La classe CSS dell’elemento DOM sottostante viene formata come prefisso `vp-` che viene aggiunto al nome del componente.

I componenti possono essere estesi o sostituiti, la loro configurazione può essere modificata e le proprietà iniziali impostate. Questo consente di avere un controllo più ampio sulle proprietà API, sul nome della classe CSS e, facoltativamente, su alcuni aspetti dell’implementazione del componente. Queste opzioni possono essere utilizzate per personalizzare le funzionalità e consentire l’utilizzo di più istanze di un componente che possono essere formattate o configurate singolarmente.

Tutte le istanze di componenti sono accessibili con la proprietà `.behaviors` . Le istanze possono essere abilitate e disabilitate, mostrate o nascoste. Tuttavia, una volta create le istanze, queste non possono essere rimosse.
