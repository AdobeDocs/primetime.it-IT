---
title: Elenco Bloccati di runtime dell’applicazione
description: Elenco Bloccati di runtime dell’applicazione
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---

# Elenco Bloccati di runtime dell’applicazione {#blocklist-of-application-runtimes}

Elenco Bloccati di runtime applicazione specifica la versione del client Primetime o del runtime di Flash che non può accedere al contenuto. Specifica il runtime con restrizioni (Flash Player, AIR o iOS), la piattaforma e la versione.

Caso d’uso di esempio: simile all’elenco Bloccati del client DRM di Primetime, è possibile specificare la versione più recente del runtime di Flash Player, AIR o iOS come versione minima richiesta per l’acquisizione della licenza e la riproduzione dei contenuti.

È possibile identificare il runtime dell&#39;applicazione in base a uno qualsiasi degli attributi supportati per le versioni del client DRM di Primetime, oltre ai seguenti attributi:

| **Attributo** | **Valori supportati** | **Corrispondenza criteri** | **Descrizione** |
|---|---|---|---|
| Applicazione | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"` | Corrispondenza esatta | Identifica il nome del runtime dell&#39;applicazione. |
