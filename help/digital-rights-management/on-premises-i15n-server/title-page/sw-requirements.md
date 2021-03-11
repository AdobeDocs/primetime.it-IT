---
title: Requisiti software
description: Requisiti software
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Requisiti software {#software-requirements}

* Tomcat 6
* JDK 1.8

## Consegna del codice / Contenuto del pacchetto{#code-delivery-package-contents}

Il pacchetto Adobe Primetime DRM On Premises Individualization Server contiene quanto segue:

* [!DNL flashaccess.war] - Il server di individuazione
* [!DNL flashaccess-kgs.war] - Server di generazione chiavi opzionale
* [!DNL /shared] - Contiene:

   * [!DNL adobe-flashaccess-certs.jar]
   * [!DNL AdobeInitial.properties] - File delle proprietà di esempio

* [!DNL thirdparty/] - Include il supporto Crypto-J come librerie native:

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] - Utility per la crittografia delle password delle credenziali del server
* [!DNL ROOT] - contiene un  [!DNL crossdomain.xml] file

* File di cache ECI - File prescaricati
* [!DNL addIndivCert.py] - Script per l’aggiornamento della directory principale di affidabilità di un server licenze per supportare le individualizzazioni in base ai prerequisiti
* [!DNL CreateMetadata.jar] - Utility per la creazione di metadati DRM in locale
* [!DNL client_sample/] - Cartella con frammento di codice client
* Note sulla versione - Per eventuali aggiunte alla documentazione dell’ultimo minuto

## Recuperare i certificati del server di individuazione{#obtain-individualization-server-certificates}

Per utilizzare il server di Individualizzazione locale on, è innanzitutto necessario ottenere due credenziali digitali (certificati):

* *Individualizzazione Crediti*  di trasporto - emessi da Adobe
* *Individualization CA Credential*  - rilasciato da Symantec (VeriSign)

Per ottenere questi certificati, invia una richiesta tramite biglietto Zendesk al seguente indirizzo: [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

Tieni presente che queste credenziali si aggiungono alle credenziali necessarie per l’utilizzo di un server licenze DRM di Primetime.