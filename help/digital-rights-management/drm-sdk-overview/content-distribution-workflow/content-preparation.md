---
description: Qualsiasi utilizzo di Adobe Primetime DRM consiste in due passaggi chiave in diversi punti del flusso di lavoro. La preparazione dei contenuti deve essere eseguita una volta per ogni risorsa e comporta la creazione di contenuti protetti. L’acquisizione dei contenuti viene eseguita più volte, una volta per ogni consumatore che desidera visualizzare tale risorsa protetta.
title: Preparazione dei contenuti
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Preparazione dei contenuti{#content-preparation}

Qualsiasi utilizzo di Adobe Primetime DRM consiste in due passaggi chiave in diversi punti del flusso di lavoro. La preparazione dei contenuti deve essere eseguita una volta per ogni risorsa e comporta la creazione di contenuti protetti. L’acquisizione dei contenuti viene eseguita più volte, una volta per ogni consumatore che desidera visualizzare tale risorsa protetta.

Prima di rendere il contenuto disponibile per la distribuzione, devi prima codificare il contenuto in formato video, creare uno o più criteri specificando le regole di utilizzo per il contenuto e creare un pacchetto con il contenuto utilizzando Adobe Primetime DRM SDK.

I passaggi per codificare, creare pacchetti e distribuire contenuti sono i seguenti:

1. Codifica il contenuto nel formato video desiderato utilizzando gli strumenti di codifica disponibili in Adobe o da terze parti.
1. Crea criteri che specificano le regole di utilizzo in base alle quali i consumatori possono visualizzare il contenuto.

   Un criterio è il contenitore delle regole e delle restrizioni che determinano come, quando e dove i contenuti protetti possono essere visualizzati dai consumatori.

   Il packager richiede almeno un criterio con almeno una regola di utilizzo. È possibile ignorare la regola di utilizzo e aggiungere regole di utilizzo aggiuntive quando il server licenze genera la licenza.

1. Crea un pacchetto per il contenuto e specifica i criteri da applicare.

   L’SDK DRM di Primetime crittografa il contenuto utilizzando una chiave di crittografia del contenuto (CEK) e lega uno o più criteri al contenuto. Il risultato è un *file di contenuto protetto *che può essere riprodotto solo da un consumatore che ha ottenuto una licenza dal corrispondente server licenze.

   Durante il packaging, il contenuto viene crittografato utilizzando il CEK. La CEK viene crittografata utilizzando la chiave pubblica del server licenze e inclusa nei metadati DRM di Primetime insieme ai criteri. I metadati DRM di Primetime vengono firmati utilizzando la chiave privata Packager e i metadati sono inclusi nel contenuto protetto.

1. Rendere i contenuti protetti disponibili per la distribuzione ai consumatori.

   Il contenuto protetto viene in genere distribuito utilizzando una rete di distribuzione dei contenuti (CDN, Content Distribution Network). La rete CDN può utilizzare qualsiasi meccanismo supportato dal runtime client, ad Flash Media Server, Adobe HTTP Dynamic Streaming per lo streaming a bit rate multiplo o un server web HTTP per il download progressivo.

