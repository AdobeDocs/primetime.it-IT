---
title: Aggiornamento del server Adobe Primetime DRM per lo streaming protetto
description: Aggiornamento del server Adobe Primetime DRM per lo streaming protetto
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Aggiornamento del server Adobe Primetime DRM per lo streaming protetto{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Se si desidera aggiornare un server che esegue Primetime DRM Server for Protected Streaming, è necessario sostituire `flashaccessserver.war` file distribuito sul server applicazioni con il file incluso con la versione più recente di Primetime DRM.

Se desideri utilizzare le nuove opzioni di configurazione, devi aggiornare i `flashaccess-tenant.xml`. È inoltre necessario aggiornare [!DNL jsafe.dll] o [!DNL libjsafe.so] con la versione inclusa con la versione più recente di Primetime DRM.
