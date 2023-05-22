---
description: Se si desidera configurare Primetime DRM, copiare i file dal DVD. Questi file includono file JAR che includono codice, certificati e classi di terze parti. Inoltre, devi richiedere un certificato ad Adobe Systems, Incorporated. Adobe rilascia quindi più credenziali utilizzate per proteggere l'integrità del contenuto del pacchetto, delle licenze e della comunicazione tra client e server.
title: Configurare l’ambiente di sviluppo
exl-id: c10f85b6-84bc-444f-9001-f49dc88cf99c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Configurare l’ambiente di sviluppo {#set-up-your-development-environment}

Se si desidera configurare Primetime DRM, copiare i file dal DVD. Questi file includono file JAR che includono codice, certificati e classi di terze parti. Inoltre, devi richiedere un certificato ad Adobe Systems, Incorporated. Adobe rilascia quindi più credenziali utilizzate per proteggere l&#39;integrità del contenuto del pacchetto, delle licenze e della comunicazione tra client e server.

L&#39;Adobe fornisce Primetime DRM SDK su DVD:

1. Copia i seguenti file da [!DNL [DVD DRM]/SDK/] al sistema di sviluppo (nel percorso di classe Java):

   * [!DNL adobe-flashaccess-certs.jar] - Include i certificati radice Adobe
   * [!DNL adobe-flashaccess-sdk.jar] - Include le classi SDK Core di Primetime DRM
   * [!DNL adobe-flashaccess-sdk-pro.jar] - Include le classi SDK professionali di Primetime DRM, necessarie solo per le funzioni professionali

1. Copia i seguenti file da [!DNL [DVD DRM]/SDK/third-party] al sistema di sviluppo:

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

1. (Facoltativo) Per migliorare le prestazioni, è possibile abilitare il supporto nativo per le operazioni di crittografia copiando la libreria specifica della piattaforma appropriata da [!DNL [DVD DRM]/SDK/thirdParty/cryptoj/] nel sistema di sviluppo (ricorda di inserire la posizione nel percorso):

   * [!DNL jsafe.dll] - Windows
   * [!DNL libjsafe.so] - Linux

      >[!NOTE]
      >
      >Sono disponibili le versioni a 32 bit e a 64 bit di queste librerie. Utilizzare la versione a 64 bit solo se si dispone di un sistema operativo a 64 bit e si esegue la versione a 64 bit di Java.

1. (Facoltativo) Per la funzionalità relativa alla compatibilità con Adobe Flash Media Rights Management Server (FMRMS) 1.x, copia `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` al sistema di sviluppo:

   Distribuisci questo solo se hai implementato in precedenza FMRMS 1.x e non desideri creare nuovamente il pacchetto del contenuto protetto da FMRMS. In questo caso, è necessario aggiungere il supporto al server licenze in modo che possa gestire i vecchi contenuti e client.
