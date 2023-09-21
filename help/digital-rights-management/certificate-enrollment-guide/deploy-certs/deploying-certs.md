---
title: Distribuire i certificati
description: Distribuire i certificati
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Distribuire i certificati{#deploy-certificates}

Per evitare che la password PFX sia disponibile in testo non crittografato sul server licenze, l&#39;implementazione di riferimento e Adobe Primetime DRM Server for Protected Streaming richiedono la crittografia della password quando specificata nel file di configurazione. Consulta *Utilizzo delle implementazioni di riferimento DRM di Primetime* o *Utilizzo del server DRM Primetime* per lo streaming protetto, per istruzioni sull&#39;esecuzione delle utilità di scrambling. Ognuna di queste include la propria utility di scramble e le password crittografate non sono intercambiabili tra queste due implementazioni di License Server.

Per distribuire i certificati e la password codificata nel server licenze, vedere *Utilizzo delle implementazioni di riferimento DRM di Primetime* o *Utilizzo del server DRM Primetime per lo streaming protetto*.
