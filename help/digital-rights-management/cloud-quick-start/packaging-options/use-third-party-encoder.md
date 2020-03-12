---
seo-title: Utilizzo di un codificatore di terze parti
title: Utilizzo di un codificatore di terze parti
uuid: 8649303c-b8e6-4c02-a8ad-5734af850bfe
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Utilizzo di un codificatore di terze parti{#use-a-third-party-encoder}

Alcuni clienti potrebbero già disporre di una pipeline per la preparazione dei contenuti, utilizzando un codificatore video hardware o software (o Adobe Media Server). In questo caso, qualsiasi prodotto che attualmente può creare contenuto protetto da DRM di Primetime può creare pacchetti di contenuto per DRM di Primetime Cloud utilizzando le stesse impostazioni di configurazione del kit di protezione DRM di Primetime Cloud. Le informazioni richieste possono essere ottenute da uno dei file di configurazione esistenti inclusi nel kit: [!DNL config_hls.xml] o [!DNL config_hds.xml].

Gli elementi di configurazione pertinenti sono:

* URL server licenze
* URL server chiave
* Certificato server licenze
* Certificato di trasporto

