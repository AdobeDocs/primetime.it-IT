---
title: Elenco Bloccati di tempi di esecuzione dell’applicazione a cui è limitato l’accesso al contenuto protetto
description: Elenco Bloccati di tempi di esecuzione dell’applicazione a cui è limitato l’accesso al contenuto protetto
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Elenco Bloccati di tempi di esecuzione dell’applicazione a cui è limitato l’accesso al contenuto protetto {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

Specifica la versione di Primetime o Flash Runtime che non può accedere al contenuto. Specifica il runtime con restrizioni (Flash Player, AIR o iOS), la piattaforma e la versione.

Caso d’uso di esempio: simile all’elenco Bloccati del client DRM, è possibile specificare la versione più recente del runtime di Flash Player, AIR o iOS come versione minima richiesta per l’acquisizione della licenza e la riproduzione dei contenuti.

Il runtime dell&#39;applicazione può essere identificato da uno qualsiasi degli attributi supportati per le versioni del client DRM, oltre ai seguenti attributi:

| **Attributo** | **Valori supportati** | **Corrispondenza criteri** | **Descrizione** |
|---|---|---|---|
| Applicazione | &quot;FlashPlayer&quot;, &quot;AIR&quot;, &quot;DRM_Library&quot;, &quot;AVE&quot; | Corrispondenza esatta | Identifica il nome del runtime dell&#39;applicazione. |
