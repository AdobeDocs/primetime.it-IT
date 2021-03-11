---
title: Installare gli strumenti della riga di comando
description: Installare gli strumenti della riga di comando
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '81'
ht-degree: 0%

---


# Installare gli strumenti della riga di comando {#install-the-command-line-tools}

1. Copia il contenuto della directory [DRM SDK DVD]\Reference Implementation\Command Line Tools\ in una directory di lavoro sul sistema.

   [!DNL .../Command Line Tools/] contenuto:

   * [!DNL flashaccesstools.properties] - Il file di configurazione predefinito per gli strumenti della riga di comando.
   * [!DNL libs/] - Contiene i file JAR degli strumenti della riga di comando
   * [!DNL samples/] - Contiene lo script della build ant (  [!DNL build-samples.xml]) e i file di origine Java.

      >[!NOTE]
      >
      >I file di origine Java mostrano come utilizzare le API SDK DRM di Primetime. Per generare ed eseguire gli esempi, esegui lo script [!DNL build-samples.xml] Ant in [!DNL samples/].