---
seo-title: File criteri DRM tra domini
title: File criteri DRM tra domini
uuid: cb91a85a-1825-4fd7-a25c-880cdbd5c8b8
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# File criteri DRM tra domini {#crossdomain-drm-policy-file}

Se il server licenze è ospitato su un dominio diverso dal file SWF di riproduzione video, è necessario un file di criteri DRM ( [!DNL crossdomain.xml]) tra più domini per consentire al file SWF di richiedere licenze da un server licenze. Un file di criteri DRM tra domini è rappresentato da un file XML che consente al server di indicare che i suoi dati e documenti sono disponibili per i file SWF gestiti da altri domini. Tutti i file SWF gestiti da un dominio specificato nel file di criteri DRM del server licenze possono accedere ai dati o alle risorse da tale server licenze.

 Adobe consiglia agli sviluppatori di seguire le procedure ottimali durante la distribuzione del file dei criteri per i domini diversi, consentendo solo ai domini trusted di accedere al server licenze e limitando l&#39;accesso alla sottodirectory della licenza sul server Web.

Per ulteriori informazioni sui file di criteri DRM tra domini, consulta le seguenti posizioni:

* Controlli del sito Web (file di criteri DRM)
* Specifica del file del criterio DRM tra domini: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

