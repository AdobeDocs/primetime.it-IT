---
description: 'null'
seo-description: 'null'
seo-title: Requisiti software
title: Requisiti software
uuid: 9faa229b-1abf-4b55-b293-247777bcb1db
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15

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
   * [!DNL AdobeInitial.properties] - Esempio di file di proprietà

* [!DNL thirdparty/] - Include il supporto Crypto-J come librerie native:

   * [!DNL libjsafe.so] (Linux)
   * [!DNL jsafe.dll] (Windows)

* [!DNL adobe-flashaccess-i15n-setup.jar] - Utility per la crittografia delle password delle credenziali del server
* [!DNL ROOT] - contiene un [!DNL crossdomain.xml] file

* File cache ECI - Precedentemente scaricati
* [!DNL addIndivCert.py] - Uno script per l&#39;aggiornamento del livello principale di affidabilità di un server licenze per il supporto delle individualizzazioni in locale
* [!DNL CreateMetadata.jar] - Utility per la creazione di metadati DRM in locale
* [!DNL client_sample/] - Una cartella con uno snippet di codice client
* Note sulla versione - Per eventuali aggiunte dell&#39;ultimo minuto alla documentazione

## Ottenere i certificati del server di individuazione{#obtain-individualization-server-certificates}

Per utilizzare On Premises Individualization Server, è innanzitutto necessario ottenere due credenziali digitali (certificati):

* *Individuazione delle credenziali* di trasporto - rilasciata da Adobe
* *Credenziale* CA per l&#39;individuazione - rilasciata da Symantec (VeriSign)

Per ottenere questi certificati, inviare una richiesta tramite biglietto Zendesk a: [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

Queste credenziali si sommano alle credenziali richieste per l&#39;utilizzo di un server licenze DRM di Primetime.