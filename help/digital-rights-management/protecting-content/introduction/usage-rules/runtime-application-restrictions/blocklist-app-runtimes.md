---
description: 'null'
seo-description: 'null'
seo-title: Blocca elenco di runtime applicazione
title: Blocca elenco di runtime applicazione
uuid: fc3c9bd6-b1e6-4534-b29c-cd9a35b80928
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Blocca elenco di runtime applicazione{#blocklist-of-application-runtimes}

L&#39;elenco dei runtime dell&#39;applicazione blocca specifica la versione del client Primetime o di Flash Runtime che non può accedere al contenuto. Specificate il runtime limitato (Flash Player, AIR o iOS), la piattaforma e la versione.

Esempio di utilizzo: Analogamente all&#39;elenco dei blocchi client DRM di Primetime, l&#39;ultima versione dei runtime Flash Player, AIR o iOS può essere specificata come versione minima richiesta per l&#39;acquisizione della licenza e la riproduzione di contenuto.

Potete identificare il runtime dell&#39;applicazione con uno degli attributi supportati per le versioni client DRM di Primetime, oltre ai seguenti attributi:

| **Attributo** | **Valori supportati** | **Criteri di corrispondenza** | **Descrizione** |
|---|---|---|---|
| Applicazione | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Corrispondenza esatta | Identifica il nome del runtime dell&#39;applicazione. |

