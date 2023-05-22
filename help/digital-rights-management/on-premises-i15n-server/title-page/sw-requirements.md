---
title: Requisiti software
description: Requisiti software
copied-description: true
exl-id: aa2ae6ac-7c2a-4cc3-a3a4-b7f92e478d23
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Requisiti software {#software-requirements}

* Tomcat 6
* JDK 1,8

## Consegna del codice/Contenuto del pacchetto{#code-delivery-package-contents}

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

## Ottenere i certificati del server di personalizzazione{#obtain-individualization-server-certificates}

Per utilizzare il server di personalizzazione locale, è necessario innanzitutto ottenere due credenziali digitali (certificati):

* *Credenziali trasporto di personalizzazione* - rilasciata dall&#39;Adobe
* *Credenziali CA di personalizzazione* - rilasciata da Symantec (VeriSign)

Per ottenere questi certificati, invia una richiesta tramite ticket Zendesk al seguente indirizzo: [https://adobeprimetime.zendesk.com](https://adobeprimetime.zendesk.com)

Queste credenziali si aggiungono alle credenziali necessarie per il funzionamento di un server licenze DRM Primetime.
