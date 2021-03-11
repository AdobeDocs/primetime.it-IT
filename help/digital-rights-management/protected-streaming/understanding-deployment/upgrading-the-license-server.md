---
title: Aggiornamento del server DRM di Adobe Primetime per lo streaming protetto
description: Aggiornamento del server DRM di Adobe Primetime per lo streaming protetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Aggiornamento del server DRM di Adobe Primetime per lo streaming protetto{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Se si desidera aggiornare un server che esegue Primetime DRM Server for Protected Streaming, è necessario sostituire il file `flashaccessserver.war` distribuito sul server dell&#39;applicazione con il file incluso con la DRM più recente di Primetime.

Se desideri utilizzare le nuove opzioni di configurazione, devi aggiornare il `flashaccess-tenant.xml` del server. È inoltre necessario aggiornare [!DNL jsafe.dll] o [!DNL libjsafe.so] con la versione inclusa con la DRM più recente di Primetime.
