---
description: 'null'
seo-description: 'null'
seo-title: ' Elenco Bloccati di tempi di esecuzione delle applicazioni'
title: ' Elenco Bloccati di tempi di esecuzione delle applicazioni'
uuid: fc3c9bd6-b1e6-4534-b29c-cd9a35b80928
translation-type: tm+mt
source-git-commit: 58bb3bedc5b0ac63afd96eb6101d9ad779e6deed
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


#  Elenco Bloccati di tempi di esecuzione delle applicazioni {#blocklist-of-application-runtimes}

 Elenco Bloccati di runtime dell&#39;applicazione specifica la versione del client Primetime o di Flash Runtime che non può accedere al contenuto. Specificate il runtime limitato (Flash Player, AIR o iOS), la piattaforma e la versione.

Esempio di utilizzo: Analogamente al elenco Bloccati di  client DRM Primetime, l&#39;ultima versione dei runtime Flash Player, AIR o iOS può essere specificata come versione minima richiesta per l&#39;acquisizione della licenza e la riproduzione di contenuto.

Potete identificare il runtime dell&#39;applicazione con uno degli attributi supportati per le versioni client DRM di Primetime, oltre ai seguenti attributi:

| **Attributo** | **Valori supportati** | **Criteri di corrispondenza** | **Descrizione** |
|---|---|---|---|
| Applicazione | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Corrispondenza esatta | Identifica il nome del runtime dell&#39;applicazione. |

