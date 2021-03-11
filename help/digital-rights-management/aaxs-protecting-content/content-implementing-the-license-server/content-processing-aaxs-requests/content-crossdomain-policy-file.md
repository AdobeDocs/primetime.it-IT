---
title: File dei criteri tra più domini
description: File dei criteri tra più domini
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# File dei criteri tra domini diversi {#crossdomain-policy-file}

Se il server licenze è ospitato su un dominio diverso dal file SWF di riproduzione video, è necessario un file di criteri tra domini diversi (crossdomain.xml) per consentire al file SWF di richiedere licenze dal server licenze. Un file di criteri tra domini diversi è un file XML che consente al server di indicare che i suoi dati e documenti sono disponibili per i file SWF provenienti da altri domini. A qualsiasi file SWF gestito da un dominio specificato nel file dei criteri di dominio del server licenze è consentito accedere ai dati o alle risorse da tale server licenze.

L’Adobe consiglia agli sviluppatori di seguire le best practice durante la distribuzione del file dei criteri tra domini diversi, consentendo solo ai domini affidabili di accedere al server licenze e limitando l’accesso alla sottodirectory delle licenze sul server web.

Per ulteriori informazioni sui file di criteri tra più domini, consulta le seguenti posizioni:

* Controlli del sito Web (file di criteri)
* Specifica del file dei criteri tra domini diversi: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

