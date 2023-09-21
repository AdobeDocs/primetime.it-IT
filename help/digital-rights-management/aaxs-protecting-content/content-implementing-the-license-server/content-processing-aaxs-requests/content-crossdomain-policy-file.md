---
title: File di criteri tra domini
description: File di criteri tra domini
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# File di criteri tra domini {#crossdomain-policy-file}

Se il server licenze è ospitato su un dominio diverso da quello del SWF di riproduzione video, è necessario un file dei criteri tra domini diversi (crossdomain.xml) per consentire al SWF di richiedere licenze al server licenze. Un file di criteri tra domini diversi è un file XML che consente al server di indicare che i dati e i documenti sono disponibili per i file SWF forniti da altri domini. Qualsiasi file SWF gestito da un dominio specificato nel file dei criteri tra domini diversi del server licenze può accedere ai dati o alle risorse da tale server licenze.

L’Adobe consiglia agli sviluppatori di seguire le best practice durante la distribuzione del file di criteri tra domini diversi, consentendo solo ai domini trusted di accedere al server licenze e limitando l’accesso alla sottodirectory della licenza sul server web.

Per ulteriori informazioni sui file delle policy tra domini, consulta i seguenti percorsi:

* Controlli del sito Web (file di criteri)
* Specifica del file di criteri tra domini: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)
