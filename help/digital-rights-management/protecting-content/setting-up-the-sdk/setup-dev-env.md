---
description: Se desiderate impostare Primetime DRM, copiate i file dal DVD. Questi file includono file JAR che includono codice, certificati e classi di terze parti. Inoltre, è necessario richiedere un certificato da  Adobe Systems, Incorporated.  Adobe quindi rilascia più credenziali da utilizzare per proteggere l'integrità del contenuto, delle licenze e della comunicazione del pacchetto tra client e server.
seo-description: Se desiderate impostare Primetime DRM, copiate i file dal DVD. Questi file includono file JAR che includono codice, certificati e classi di terze parti. Inoltre, è necessario richiedere un certificato da  Adobe Systems, Incorporated.  Adobe quindi rilascia più credenziali da utilizzare per proteggere l'integrità del contenuto, delle licenze e della comunicazione del pacchetto tra client e server.
seo-title: Configurare l'ambiente di sviluppo
title: Configurare l'ambiente di sviluppo
uuid: 68afefe8-7ec6-466e-89a8-bc0da8afb4c8
translation-type: tm+mt
source-git-commit: 19e7c941b3337c3b4d37f0b6a1350aac2ad8a0cc
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# Configurare l&#39;ambiente di sviluppo {#set-up-your-development-environment}

Se desiderate impostare Primetime DRM, copiate i file dal DVD. Questi file includono file JAR che includono codice, certificati e classi di terze parti. Inoltre, è necessario richiedere un certificato da  Adobe Systems, Incorporated.  Adobe quindi rilascia più credenziali da utilizzare per proteggere l&#39;integrità del contenuto, delle licenze e della comunicazione del pacchetto tra client e server.

 Adobe fornisce l’SDK DRM Primetime su DVD:

1. Copiate i seguenti file da [!DNL [DRM DVD]/SDK/] al sistema di sviluppo (nel percorso di classe Java):

   * [!DNL adobe-flashaccess-certs.jar] - Include  certificati radice Adobe
   * [!DNL adobe-flashaccess-sdk.jar] - Include le classi SDK di base Primetime DRM
   * [!DNL adobe-flashaccess-sdk-pro.jar] - Include le classi SDK Primetime DRM Professional, richieste solo per le funzioni Professional

1. Copiate i seguenti file da [!DNL [DRM DVD]/SDK/third-party] al sistema di sviluppo:

   * [!DNL bcmail-jdk15-141.jar]
   * [!DNL bcprov-jdk15-141.jar]
   * [!DNL commons-discovery-0.4.jar]
   * [!DNL commons-logging-1.1.1.jar]
   * [!DNL cryptoj.jar]
   * [!DNL jaxb-api.jar]
   * [!DNL jaxb-impl.jar]
   * [!DNL jaxb-libs.jar]
   * [!DNL relaxngDatatype.jar]
   * [!DNL rm-pdrl.jar]
   * [!DNL xsdlib.jar]
   * [!DNL jackson-annotations-2.4.0-rc4-20140522.175222-3.jar]
   * [!DNL jackson-core--2.4.0-rc4-20140529.184520-13.jar]
   * [!DNL jackson-databind-2.4.0-rc4-20140603.005043-38.jar]

1. (Facoltativo) Per migliorare le prestazioni, è possibile abilitare il supporto nativo per le operazioni di crittografia copiando la libreria specifica della piattaforma appropriata da [!DNL [DRM DVD]/SDK/thirdparty/cryptoj/] nel sistema di sviluppo (ricordate di inserire la posizione nel percorso):

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >Sono disponibili versioni a 32 bit e a 64 bit di queste librerie. È consigliabile utilizzare la versione a 64 bit solo se si dispone di un sistema operativo a 64 bit e si esegue la versione a 64 bit di Java.

1. (Facoltativo) Per le funzionalità correlate alla compatibilità  Adobe Media Rights Management Flash Server (FMRMS) 1.x, copiate `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` nel sistema di sviluppo:

   Distribuire questa funzionalità solo se in precedenza è stato distribuito FMRMS 1.x e non si desidera creare nuovamente il pacchetto dei contenuti protetti FMRMS. In questo caso, è necessario aggiungere questo supporto al server delle licenze in modo che possa gestire vecchi contenuti e client.
