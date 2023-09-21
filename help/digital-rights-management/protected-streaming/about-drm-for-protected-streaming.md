---
description: Adobe Primetime DRM Server for Protected Streaming è un'implementazione del server di licenze basata sull'SDK di Primetime DRM. Questo server rilascia licenze per contenuti protetti ai client DRM Primetime.
title: Informazioni su Adobe Primetime DRM Server per lo streaming protetto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Informazioni su Adobe Primetime DRM Server per lo streaming protetto{#about-adobe-primetime-drm-server-for-protected-streaming}

Adobe Primetime DRM Server for Protected Streaming è un&#39;implementazione del server di licenze basata sull&#39;SDK di Primetime DRM. Questo server rilascia licenze per contenuti protetti ai client DRM Primetime.

Il server DRM Primetime per lo streaming protetto supporta più tenant. È possibile ospitare un singolo server per conto di più autori di contenuti, ciascuno con le proprie impostazioni di configurazione. Inoltre, il server supporta componenti di autorizzazione personalizzati, che consentono di eseguire una logica personalizzata prima dell&#39;emissione di una licenza.

Questo server è destinato all&#39;utilizzo con Streaming HTTP. Di conseguenza, questa implementazione del server non supporta tutte le funzionalità disponibili in DRM di Primetime. Ad esempio, non supporta le richieste di autenticazione degli utenti, più criteri, licenze a livello di dominio, concatenamento delle licenze o messaggi di sincronizzazione.

>[!NOTE]
>
>Adobe Primetime DRM era precedentemente denominato Adobe Access e, prima di questo, Flash Access.
