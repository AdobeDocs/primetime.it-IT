---
seo-title: Aggiornamento del server Adobe Primetime DRM per lo streaming protetto
title: Aggiornamento del server Adobe Primetime DRM per lo streaming protetto
uuid: 5c507ae3-d1d9-40ad-ba97-501ec92b45dc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Aggiornamento del server Adobe Primetime DRM per lo streaming protetto{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Se si desidera aggiornare un server che esegue Primetime DRM Server for Protected Streaming, è necessario sostituire il `flashaccessserver.war` file distribuito sul server applicazioni con il file incluso con la DRM di Primetime più recente.

Per utilizzare le nuove opzioni di configurazione, è necessario aggiornare quelle del server `flashaccess-tenant.xml`. È inoltre necessario eseguire l&#39;aggiornamento [!DNL jsafe.dll] o [!DNL libjsafe.so] con la versione inclusa con l&#39;ultima DRM di Primetime.
