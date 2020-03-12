---
description: Per utilizzare Browser TVSDK, è necessario creare e configurare un lettore di base. Per la riproduzione di contenuti video, potete creare un lettore di base in due modi, utilizzando il browser TVSDK o il framework dell'interfaccia utente.
seo-description: Per utilizzare Browser TVSDK, è necessario creare e configurare un lettore di base. Per la riproduzione di contenuti video, potete creare un lettore di base in due modi, utilizzando il browser TVSDK o il framework dell'interfaccia utente.
seo-title: Lettore base
title: Lettore base
uuid: 44a27458-be12-452f-92b9-3cef79439257
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Panoramica {#basic-player-overview}

Per utilizzare Browser TVSDK, è necessario creare e configurare un lettore di base. Per la riproduzione di contenuti video, potete creare un lettore di base in uno dei due modi seguenti: utilizzare il browser TVSDK o il framework dell&#39;interfaccia utente.

## Utilizzo del browser TVSDK {#section_4D1C6D4B3A3447DFA2AA0229E140E2D9}

Utilizzate le API fornite con l&#39;SDK per browser direttamente per codificare il lettore video. L’SDK fornisce framework e utility, nonché un lettore di riferimento da cui lavorare.

>[!TIP]
>
>Per visualizzare questo funzionamento in un lettore di riferimento, non specificate alcun attributo con `videoDiv`.

## Utilizzo del framework dell&#39;interfaccia utente {#section_AE02384CFEF64A448C108232AB62A9FF}

Questo modulo viene utilizzato per creare istanze del lettore, in cui ogni istanza è associata a un elemento DOM (Document Object Model) fornito dal chiamante. Oltre ad avere un&#39;istanza del Browser TVSDK, ogni istanza del lettore ospita una serie di controlli che costituiscono l&#39;interfaccia utente del lettore.

L&#39;attuazione di ciascun controllo è articolata in due aspetti:

* Una `HTMLElement`, che è la rappresentazione visiva del componente sullo schermo
* A, che gestisce `Behavior``HTMLElement` e fornisce un&#39;API per le interazioni

I dettagli relativi a questi controlli vengono forniti all&#39;utente `VideoPlayer` utilizzando un oggetto config, che viene passato al lettore all&#39;istanza. Per impostazione predefinita, ogni componente forma una gerarchia di oggetti, con l&#39;elemento fornito all&#39;istanza del lettore alla radice della struttura. Man mano che viene creato, ciascun componente viene aggiunto al DOM nella posizione appropriata.

Ogni componente ha un nome, che è la chiave nell&#39;oggetto config quando l&#39;oggetto è registrato. La classe CSS dell’elemento DOM sottostante è formata come `vp-` prefisso che viene aggiunto al nome del componente.

I componenti possono essere estesi o sostituiti, la loro configurazione può essere modificata e le proprietà iniziali impostate. Questo consente di avere un controllo più ampio sulle proprietà API, sul nome della classe CSS e, facoltativamente, su alcuni aspetti dell&#39;implementazione del componente. Queste opzioni possono essere utilizzate per personalizzare le funzionalità e consentire più istanze di un componente che possono essere formattate o configurate singolarmente.

È possibile accedere a tutte le istanze dei componenti con la `.behaviors` proprietà. Le istanze possono essere abilitate e disattivate e visualizzate o nascoste. Tuttavia, una volta create le istanze, queste non possono essere rimosse.
