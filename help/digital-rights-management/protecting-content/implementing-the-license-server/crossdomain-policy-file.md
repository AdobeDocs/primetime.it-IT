---
title: File di criteri DRM tra domini
description: File di criteri DRM tra domini
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# File di criteri DRM tra domini {#crossdomain-drm-policy-file}

Se il server licenze è ospitato su un dominio diverso rispetto al SWF di riproduzione video, viene creato un file di criteri DRM tra domini diversi ( [!DNL crossdomain.xml]) è necessario per consentire al SWF di richiedere licenze da un server licenze. Un file di criteri DRM tra domini diversi è rappresentato da un file XML che consente al server di indicare che i relativi dati e documenti sono disponibili per i file SWF forniti da altri domini. Qualsiasi file SWF gestito da un dominio specificato nel file dei criteri DRM del server licenze tra domini diversi può accedere ai dati o alle risorse da tale server licenze.

L’Adobe consiglia agli sviluppatori di seguire le best practice durante la distribuzione del file di criteri tra domini diversi, consentendo solo ai domini trusted di accedere al server licenze e limitando l’accesso alla sottodirectory della licenza sul server web.

Per ulteriori informazioni sui file dei criteri DRM tra domini, vedere i percorsi seguenti:

* Controlli del sito Web (file di criteri DRM)
* Specifica del file di criteri DRM tra domini: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

