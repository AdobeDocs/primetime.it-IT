---
title: Generazione di numeri casuali
description: Generazione di numeri casuali
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---

# Generazione di numeri casuali{#generating-random-numbers}

I generatori di numeri casuali hardware possono essere utilizzati sui server Linux per garantire che venga generata un&#39;entropia sufficiente. Se la macchina non è in grado di generare abbastanza entropia, le operazioni Adobe Access che richiedono una fonte di casualità si bloccheranno in attesa dei dati da `/dev/random`.
