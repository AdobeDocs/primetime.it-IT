---
seo-title: Aggiornamento del  Adobe Primetime DRM Server per lo streaming protetto
title: Aggiornamento del  Adobe Primetime DRM Server per lo streaming protetto
uuid: 5c507ae3-d1d9-40ad-ba97-501ec92b45dc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---


# Aggiornamento del server DRM  Adobe Primetime per lo streaming protetto{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

Se si desidera aggiornare un server che esegue Primetime DRM Server for Protected Streaming, è necessario sostituire il file `flashaccessserver.war` distribuito sul server dell&#39;applicazione con il file che è stato incluso con la DRM di Primetime più recente.

Per utilizzare le nuove opzioni di configurazione, è necessario aggiornare il `flashaccess-tenant.xml` del server. È inoltre necessario aggiornare [!DNL jsafe.dll] o [!DNL libjsafe.so] con la versione inclusa con l&#39;ultima DRM di Primetime.
