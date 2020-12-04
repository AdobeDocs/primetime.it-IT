---
seo-title: File di criteri tra domini
title: File di criteri tra domini
uuid: fc05aa5e-6fbd-445f-a22a-f795d5a0b3ad
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# File di criteri tra domini {#crossdomain-policy-file}

Se il server licenze è ospitato su un dominio diverso dal file SWF di riproduzione video, è necessario un file di criteri per i domini diversi (crossdomain.xml) per consentire al file SWF di richiedere licenze al server licenze. Un file di criteri validi per più domini è un file XML che consente al server di indicare che i relativi dati e documenti sono disponibili per i file SWF gestiti da altri domini. Tutti i file SWF gestiti da un dominio specificato nel file dei criteri per i domini del server licenze possono accedere ai dati o alle risorse provenienti da tale server licenze.

 Adobe consiglia agli sviluppatori di seguire le procedure ottimali durante la distribuzione del file dei criteri per i domini diversi, consentendo solo ai domini trusted di accedere al server licenze e limitando l&#39;accesso alla sottodirectory della licenza sul server Web.

Per ulteriori informazioni sui file dei criteri per i domini, consulta i seguenti percorsi:

* Controlli del sito Web (file dei criteri)
* Specifica del file dei criteri per i domini: [https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html](https://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)

