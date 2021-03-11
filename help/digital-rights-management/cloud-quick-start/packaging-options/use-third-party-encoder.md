---
title: Utilizzare un codificatore di terze parti
description: Utilizzare un codificatore di terze parti
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Utilizza un codificatore di terze parti{#use-a-third-party-encoder}

Alcuni clienti potrebbero già disporre di una pipeline di preparazione dei contenuti, utilizzando un codificatore video hardware o software (o Adobe Medium Server). In questo caso, qualsiasi prodotto che attualmente può creare contenuti protetti da DRM di Primetime può creare pacchetti di contenuti per DRM di Primetime Cloud utilizzando le stesse impostazioni di configurazione del kit di protezione DRM di Primetime Cloud. Le informazioni richieste possono essere ottenute da uno dei file di configurazione esistenti inclusi nel kit: [!DNL config_hls.xml] o [!DNL config_hds.xml].

Gli elementi di configurazione rilevanti sono:

* URL server licenze
* URL server chiave
* Certificato del server licenze
* Certificato di trasporto

