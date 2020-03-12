---
seo-title: Consegna del codice / Contenuto del pacchetto
title: Consegna del codice / Contenuto del pacchetto
uuid: 13de2fd4-9079-496c-a087-25176c118864
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Consegna del codice / Contenuto del pacchetto{#code-delivery-package-contents}

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

