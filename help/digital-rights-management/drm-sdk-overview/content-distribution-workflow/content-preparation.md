---
description: Qualsiasi utilizzo di  Adobe Primetime DRM consiste di due passaggi fondamentali in diversi punti del flusso di lavoro. La preparazione del contenuto deve essere eseguita una volta per ogni risorsa e i risultati possono creare contenuto protetto. L'acquisizione dei contenuti viene eseguita più volte, una volta per ogni consumatore che desidera visualizzare la risorsa protetta.
seo-description: Qualsiasi utilizzo di  Adobe Primetime DRM consiste di due passaggi fondamentali in diversi punti del flusso di lavoro. La preparazione del contenuto deve essere eseguita una volta per ogni risorsa e i risultati possono creare contenuto protetto. L'acquisizione dei contenuti viene eseguita più volte, una volta per ogni consumatore che desidera visualizzare la risorsa protetta.
seo-title: Preparazione dei contenuti
title: Preparazione dei contenuti
uuid: edb633f0-b623-41ea-a52a-19017d45fb18
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# Preparazione dei contenuti{#content-preparation}

Qualsiasi utilizzo di  Adobe Primetime DRM consiste di due passaggi fondamentali in diversi punti del flusso di lavoro. La preparazione del contenuto deve essere eseguita una volta per ogni risorsa e i risultati possono creare contenuto protetto. L&#39;acquisizione dei contenuti viene eseguita più volte, una volta per ogni consumatore che desidera visualizzare la risorsa protetta.

Prima di rendere il contenuto disponibile per la distribuzione, è necessario codificare il contenuto in formato video, creare uno o più criteri che specifichino le regole di utilizzo per il contenuto e creare pacchetti di contenuto utilizzando  SDK Adobe Primetime DRM.

Per codificare, creare pacchetti e distribuire contenuti, effettuate le seguenti operazioni:

1. Codificate il contenuto nel formato video desiderato utilizzando gli strumenti di codifica disponibili  Adobe o da terze parti.
1. Creare criteri che specificano le regole di utilizzo in base alle quali i consumatori possono visualizzare il contenuto.

   Un criterio è il contenitore delle regole e delle restrizioni che determinano come, quando e dove i contenuti protetti possono essere visualizzati dai consumatori.

   Il packager richiede almeno un criterio con almeno una regola di utilizzo. È possibile ignorare la regola di utilizzo e aggiungere ulteriori regole di utilizzo quando il server licenze genera la licenza.

1. Create un pacchetto del contenuto e specificate i criteri da applicare.

   Primetime DRM SDK crittografa il contenuto utilizzando una chiave di crittografia dei contenuti (CEK) e vincola uno o più criteri al contenuto. Il risultato è un *file di contenuto protetto *che può essere riprodotto solo da un consumatore che ha ottenuto una licenza dal server licenze corrispondente.

   Durante la creazione del pacchetto, il contenuto viene cifrato utilizzando CEK. Il CEK viene crittografato utilizzando la chiave pubblica del server licenze e viene incluso nei metadati DRM di Primetime insieme ai criteri. I metadati DRM di Primetime vengono firmati utilizzando la chiave privata di Packager e i metadati sono inclusi nel contenuto protetto.

1. Rendere il contenuto protetto disponibile per la distribuzione ai consumatori.

   Il contenuto protetto viene in genere distribuito tramite una rete di distribuzione di contenuti (CDN). Il CDN può utilizzare qualsiasi meccanismo supportato dal runtime client, ad esempio Flash Media Server, HTTP Dynamic Streaming Adobe  per lo streaming con bitrate multiplo o un server Web HTTP per lo scaricamento progressivo.

