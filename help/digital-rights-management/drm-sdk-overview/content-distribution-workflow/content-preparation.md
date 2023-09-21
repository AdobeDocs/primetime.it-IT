---
description: Qualsiasi utilizzo di Adobe Primetime DRM è costituito da due passaggi chiave in punti diversi del flusso di lavoro. La preparazione dei contenuti deve essere eseguita una volta per ogni risorsa e comporta la creazione di contenuto protetto. L’acquisizione dei contenuti viene eseguita più volte, una volta per ogni consumatore che desidera guardare la risorsa protetta.
title: Preparazione dei contenuti
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Preparazione dei contenuti{#content-preparation}

Qualsiasi utilizzo di Adobe Primetime DRM è costituito da due passaggi chiave in punti diversi del flusso di lavoro. La preparazione dei contenuti deve essere eseguita una volta per ogni risorsa e comporta la creazione di contenuto protetto. L’acquisizione dei contenuti viene eseguita più volte, una volta per ogni consumatore che desidera guardare la risorsa protetta.

Prima di rendere il contenuto disponibile per la distribuzione, è necessario codificarlo nel formato video, creare uno o più criteri che specifichino le regole di utilizzo per il contenuto e creare un pacchetto del contenuto utilizzando l’SDK Adobe Primetime DRM.

I passaggi per codificare, creare pacchetti e distribuire il contenuto sono i seguenti:

1. Codifica il contenuto nel formato video desiderato utilizzando gli strumenti di codifica disponibili presso Adobe o terze parti.
1. Creare criteri che specificano le regole di utilizzo in base alle quali i consumatori possono visualizzare il contenuto.

   Una policy è il contenitore delle regole e delle restrizioni che determinano come, quando e dove i contenuti protetti possono essere visualizzati dai consumatori.

   Il packager richiede almeno un criterio con almeno una regola di utilizzo. È possibile ignorare la regola di utilizzo e aggiungere altre regole di utilizzo quando il server licenze genera la licenza.

1. Crea un pacchetto del contenuto e specifica i criteri da applicare.

   L’SDK DRM di Primetime crittografa il contenuto utilizzando una chiave di crittografia del contenuto (CEK) e associa uno o più criteri al contenuto. Il risultato è un *file di contenuto protetto *che può essere riprodotto solo da un consumatore che ha ottenuto una licenza dal server licenze corrispondente.

   Durante la creazione del pacchetto, il contenuto viene crittografato utilizzando il codice di archiviazione. Il codice CEK viene crittografato utilizzando la chiave pubblica del server licenze e incluso nei metadati DRM di Primetime insieme ai criteri. I metadati DRM di Primetime sono firmati utilizzando la chiave privata Packager e sono inclusi nel contenuto protetto.

1. Rendere i contenuti protetti disponibili per la distribuzione ai consumatori.

   Il contenuto protetto viene in genere distribuito utilizzando una rete di distribuzione del contenuto (CDN, content distribution network). La rete CDN può utilizzare qualsiasi meccanismo supportato dal runtime client, ad esempio Flash Media Server, HTTP Dynamic Streaming Adobe per lo streaming con bitrate multiplo o un server web HTTP per il download progressivo.
