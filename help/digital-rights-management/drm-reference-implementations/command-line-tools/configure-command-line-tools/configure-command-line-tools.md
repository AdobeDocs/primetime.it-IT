---
seo-title: Configurare ed eseguire gli strumenti della riga di comando
title: Configurare ed eseguire gli strumenti della riga di comando
uuid: b65f8621-54fa-4927-b2f4-d2fd60350fc1
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# Configurare ed eseguire gli strumenti della riga di comando {#configure-and-run-the-command-line-tools}

Agli strumenti della riga di comando sono associate proprietà per le quali è necessario impostare i valori in [!DNL flashaccesstools.properties] *prima di* eseguire gli strumenti. Alcuni degli strumenti della riga di comando consentono inoltre di specificare i valori delle proprietà dalla riga di comando. I valori specificati dalla riga di comando hanno la precedenza rispetto ai valori forniti da [!DNL flashaccesstools.properties].

È necessario modificare le impostazioni nelle seguenti sezioni di [!DNL flashaccesstools.properties] per attivare gli strumenti della riga di comando corrispondenti che si intende utilizzare:

* **Proprietà**  di Media Packager - (per  [!DNL AdobePackager.jar])

* **Gestione elenco aggiornamenti criteri e proprietà**  Gestione elenco revoca - (per  [!DNL AdobePolicyUpdateListManager.jar] e  [!DNL AdobeRevocationListManager.jar])

* **Proprietà**  del Gestore dei criteri - (per  [!DNL AdobePolicyManager.jar])

* **Proprietà**  del generatore di licenze - (per  [!DNL AdobeLicenseGenerator.jar])