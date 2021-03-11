---
title: Elenco Bloccati di runtime di applicazioni
description: Elenco Bloccati di runtime di applicazioni
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Elenco Bloccati di runtime di applicazioni {#blocklist-of-application-runtimes}

Elenco Bloccati di runtime dell’applicazione specifica la versione del client Primetime o di Flash Runtime che non può accedere al contenuto. Specifica il runtime limitato (Flash Player, AIR o iOS), la piattaforma e la versione.

Esempio di utilizzo: Analogamente all’elenco Bloccati client DRM di Primetime, è possibile specificare come versione minima necessaria per l’acquisizione della licenza e la riproduzione dei contenuti la versione più recente dei tempi di esecuzione di Flash Player, AIR o iOS.

È possibile identificare il runtime dell’applicazione mediante uno qualsiasi degli attributi supportati per le versioni client DRM di Primetime, oltre ai seguenti attributi:

| **Attributo** | **Valori supportati** | **Criteri di corrispondenza** | **Descrizione** |
|---|---|---|---|
| Applicazione | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Corrispondenza esatta | Identifica il nome del runtime dell&#39;applicazione. |

