---
description: Se si desidera impostare Primetime DRM, copiare i file dal DVD. Questi file includono file JAR che includono codice, certificati e classi di terze parti. Inoltre, devi richiedere un certificato ad Adobe Systems, Incorporated. L'Adobe invia quindi più credenziali utilizzate per proteggere l'integrità del contenuto, delle licenze e della comunicazione in pacchetto tra client e server.
title: Configurare l’ambiente di sviluppo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Configurare l&#39;ambiente di sviluppo {#set-up-your-development-environment}

Se si desidera impostare Primetime DRM, copiare i file dal DVD. Questi file includono file JAR che includono codice, certificati e classi di terze parti. Inoltre, devi richiedere un certificato ad Adobe Systems, Incorporated. L&#39;Adobe invia quindi più credenziali utilizzate per proteggere l&#39;integrità del contenuto, delle licenze e della comunicazione in pacchetto tra client e server.

Adobe fornisce l&#39;SDK DRM di Primetime su DVD:

1. Copia i seguenti file da [!DNL [DRM DVD]/SDK/] al tuo sistema di sviluppo (sul tuo percorso di classe Java):

   * [!DNL adobe-flashaccess-certs.jar] - Include i certificati radice di Adobe
   * [!DNL adobe-flashaccess-sdk.jar] - Include le classi SDK di base DRM di Primetime
   * [!DNL adobe-flashaccess-sdk-pro.jar] - Include le classi SDK Primetime DRM Professional, richieste solo per le funzioni Professional

1. Copia i seguenti file da [!DNL [DRM DVD]/SDK/thirdparty] al tuo sistema di sviluppo:

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

1. (Facoltativo) Per migliorare le prestazioni, è possibile abilitare il supporto nativo per le operazioni di crittografia copiando la libreria specifica della piattaforma appropriata da [!DNL [DRM DVD]/SDK/thirdparty/cryptoj/] al sistema di sviluppo (ricorda di posizionare la posizione sul percorso):

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >Sono disponibili versioni a 32 bit e a 64 bit di queste librerie. Usa la versione a 64 bit solo se hai un sistema operativo a 64 bit ed esegui la versione a 64 bit di Java.

1. (Facoltativo) Per le funzionalità relative alla compatibilità di Adobe Flash Media Rights Management Server (FMRMS) 1.x, copia `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` nel tuo sistema di sviluppo:

   Distribuisci solo se hai implementato in precedenza FMRMS 1.x e non desideri ricompilare il contenuto protetto da FMRMS. In questo caso, devi aggiungere questo supporto al server licenze in modo che possa gestire i vecchi contenuti e client.
