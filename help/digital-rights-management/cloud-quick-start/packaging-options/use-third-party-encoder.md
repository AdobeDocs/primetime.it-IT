---
title: Utilizzare un codificatore di terze parti
description: Utilizzare un codificatore di terze parti
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Utilizzare un codificatore di terze parti{#use-a-third-party-encoder}

Alcuni clienti possono già disporre di una pipeline di preparazione dei contenuti che utilizza un codificatore video (o un Adobe Media Server) hardware o software. In questo caso, qualsiasi prodotto che possa creare contenuti protetti da Primetime DRM può creare pacchetti di contenuti per Primetime Cloud DRM utilizzando le stesse impostazioni di configurazione del kit di protezione Primetime Cloud DRM. Le informazioni richieste possono essere ottenute da uno dei file di configurazione esistenti inclusi nel kit: [!DNL config_hls.xml] o [!DNL config_hds.xml].

Gli elementi di configurazione rilevanti sono:

* URL server licenze
* URL server chiave
* Certificato server licenze
* Certificato di trasporto
