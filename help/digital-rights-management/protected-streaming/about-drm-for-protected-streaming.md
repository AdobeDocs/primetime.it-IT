---
description: Il server DRM di Adobe Primetime per lo streaming protetto è un'implementazione del server di licenze basata sull'SDK DRM di Primetime. Questo server rilascia licenze per contenuti protetti ai client DRM di Primetime.
title: Informazioni sul server DRM di Adobe Primetime per lo streaming protetto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Informazioni sul server DRM Adobe Primetime per lo streaming protetto{#about-adobe-primetime-drm-server-for-protected-streaming}

Il server DRM di Adobe Primetime per lo streaming protetto è un&#39;implementazione del server di licenze basata sull&#39;SDK DRM di Primetime. Questo server rilascia licenze per contenuti protetti ai client DRM di Primetime.

Il server DRM di Primetime per lo streaming protetto supporta più tenant. È possibile ospitare un singolo server per conto di più editori di contenuti, ciascuno con le proprie impostazioni di configurazione. Inoltre, il server supporta componenti di autorizzazione personalizzati, per cui puoi eseguire logica personalizzata prima che venga rilasciata una licenza.

Questo server è destinato all&#39;utilizzo con HTTP Streaming. Di conseguenza, questa implementazione del server non supporta tutte le funzionalità disponibili in DRM di Primetime. Ad esempio, non supporta le richieste di autenticazione degli utenti, più criteri, licenze associate al dominio, concatenamento licenze o messaggi di sincronizzazione.

>[!NOTE]
>
>Adobe Primetime DRM era precedentemente denominato accesso Adobe e prima di tale Flash Access.

