---
title: Configurare ed eseguire gli strumenti della riga di comando
description: Configurare ed eseguire gli strumenti della riga di comando
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Configurare ed eseguire gli strumenti della riga di comando {#configure-and-run-the-command-line-tools}

Gli strumenti della riga di comando hanno proprietà associate per le quali è necessario impostare i valori in [!DNL flashaccesstools.properties] *prima di* esegui gli strumenti. Alcuni strumenti della riga di comando consentono inoltre di specificare i valori delle proprietà dalla riga di comando. I valori specificati dalla riga di comando hanno la precedenza su quelli forniti da [!DNL flashaccesstools.properties].

È necessario modificare le impostazioni nelle sezioni seguenti di [!DNL flashaccesstools.properties] per attivare gli strumenti della riga di comando corrispondenti che si intende utilizzare:

* **Proprietà Media Packager** - (per [!DNL AdobePackager.jar])

* **Proprietà di Gestione elenchi aggiornamento criteri e Gestione elenchi di revoche** - (per [!DNL AdobePolicyUpdateListManager.jar] e [!DNL AdobeRevocationListManager.jar])

* **Proprietà di Policy Manager** - (per [!DNL AdobePolicyManager.jar])

* **Proprietà generatore di licenze** - (per [!DNL AdobeLicenseGenerator.jar])
