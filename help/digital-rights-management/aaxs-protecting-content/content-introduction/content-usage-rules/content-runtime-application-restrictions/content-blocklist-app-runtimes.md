---
title: Elenco Bloccati di runtime di applicazioni con restrizioni all’accesso a contenuti protetti
description: Elenco Bloccati di runtime di applicazioni con restrizioni all’accesso a contenuti protetti
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Elenco Bloccati di runtime di applicazioni con restrizioni all’accesso a contenuti protetti {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

Specifica la versione di Primetime o Flash Runtime che non può accedere al contenuto. Specifica il runtime limitato (Flash Player, AIR o iOS), la piattaforma e la versione.

Esempio di utilizzo: Analogamente all’elenco Bloccati client DRM, è possibile specificare come versione minima necessaria per l’acquisizione della licenza e la riproduzione di contenuti la versione più recente dei tempi di esecuzione di Flash Player, AIR o iOS.

Il runtime dell’applicazione può essere identificato da uno qualsiasi degli attributi supportati per le versioni client DRM, oltre ai seguenti attributi:

| **Attributo** | **Valori supportati** | **Criteri di corrispondenza** | **Descrizione** |
|---|---|---|---|
| Applicazione | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Corrispondenza esatta | Identifica il nome del runtime dell&#39;applicazione. |
