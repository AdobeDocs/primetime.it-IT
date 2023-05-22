---
title: Consegna del codice/Contenuto del pacchetto
description: Consegna del codice/Contenuto del pacchetto
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Consegna del codice/Contenuto del pacchetto{#code-delivery-package-contents}

Il pacchetto Adobe Primetime DRM On Premises Individualization Server contiene quanto segue:

* [!DNL flashaccess.war] - Server di personalizzazione
* [!DNL flashaccess-kgs.war] - Server di generazione di chiavi opzionale
* [!DNL /shared] - Contiene:

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties] - File delle proprietà di esempio

* [!DNL thirdparty/] - Include il supporto di Crypto-J come librerie native:

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] - Utility per la crittografia delle password delle credenziali del server
* [!DNL ROOT] - contiene un [!DNL crossdomain.xml] file

* File cache ECI - Pre-scaricati
* [!DNL addIndivCert.py] - Script per aggiornare la radice di attendibilità di un server licenze per supportare le individualizzazioni locali
* [!DNL CreateMetadata.jar] - Utility per la creazione di metadati DRM locali
* [!DNL client_sample/] : cartella con uno snippet di codice client
* Note sulla versione - Per eventuali aggiunte dell’ultimo minuto alla documentazione

