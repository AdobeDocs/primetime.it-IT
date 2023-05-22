---
title: Generazione di numeri casuali
description: Generazione di numeri casuali
copied-description: true
exl-id: 9a816570-753e-4b05-a6ea-2d4b20ffa3d4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# Generazione di numeri casuali{#generating-random-numbers}

I generatori di numeri casuali hardware possono essere utilizzati sui server Linux per garantire che venga generata un&#39;entropia sufficiente. Se la macchina non è in grado di generare abbastanza entropia, le operazioni Adobe Access che richiedono una fonte di casualità si bloccheranno in attesa dei dati da `/dev/random`.
