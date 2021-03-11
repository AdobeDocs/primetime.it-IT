---
title: Generazione di numeri casuali
description: Generazione di numeri casuali
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---


# Generazione di numeri casuali{#generating-random-numbers}

I generatori di numeri casuali hardware possono essere utilizzati sui server Linux per garantire che venga generata un&#39;entropia sufficiente. Se la macchina non è in grado di generare abbastanza entropia, le operazioni di accesso Adobe che richiedono un&#39;origine di casualità verranno bloccate in attesa dei dati da `/dev/random`.
