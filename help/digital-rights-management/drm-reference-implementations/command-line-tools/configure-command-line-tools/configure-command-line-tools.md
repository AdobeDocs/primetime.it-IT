---
title: Configurare ed eseguire gli strumenti della riga di comando
description: Configurare ed eseguire gli strumenti della riga di comando
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# Configurare ed eseguire gli strumenti della riga di comando {#configure-and-run-the-command-line-tools}

Gli strumenti della riga di comando dispongono di proprietà associate per le quali è necessario impostare i valori in [!DNL flashaccesstools.properties] *prima di* eseguire gli strumenti. Alcuni degli strumenti della riga di comando consentono inoltre di specificare i valori delle proprietà dalla riga di comando. I valori specificati dalla riga di comando hanno la precedenza sui valori forniti da [!DNL flashaccesstools.properties].

È necessario modificare le impostazioni nelle sezioni seguenti di [!DNL flashaccesstools.properties] per abilitare gli strumenti della riga di comando corrispondenti che si intende utilizzare:

* **Proprietà**  Media Packager - (per  [!DNL AdobePackager.jar])

* **Proprietà**  di Gestione elenchi aggiornamenti criteri e Gestione elenchi revoche - (per  [!DNL AdobePolicyUpdateListManager.jar] e  [!DNL AdobeRevocationListManager.jar])

* **Proprietà**  di Policy Manager - (per  [!DNL AdobePolicyManager.jar])

* **Proprietà**  del generatore di licenze - (per  [!DNL AdobeLicenseGenerator.jar])