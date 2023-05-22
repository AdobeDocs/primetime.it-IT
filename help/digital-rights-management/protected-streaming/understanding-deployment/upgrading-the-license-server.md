---
title: Aggiornamento del server Adobe Primetime DRM per lo streaming protetto
description: Aggiornamento del server Adobe Primetime DRM per lo streaming protetto
copied-description: true
exl-id: 6edfba1b-46a2-4cbd-bc14-feeef1a36ed6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Aggiornamento del server Adobe Primetime DRM per lo streaming protetto{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Se si desidera aggiornare un server che esegue Primetime DRM Server for Protected Streaming, è necessario sostituire `flashaccessserver.war` file distribuito sul server applicazioni con il file incluso con la versione più recente di Primetime DRM.

Se desideri utilizzare le nuove opzioni di configurazione, devi aggiornare i `flashaccess-tenant.xml`. È inoltre necessario aggiornare [!DNL jsafe.dll] o [!DNL libjsafe.so] con la versione inclusa con la versione più recente di Primetime DRM.
