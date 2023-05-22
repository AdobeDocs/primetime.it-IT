---
title: Flusso di lavoro tipico
description: Flusso di lavoro tipico
copied-description: true
exl-id: c2020b48-7e97-4df5-a453-7b76e2e1d458
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Flusso di lavoro tipico{#typical-workflow}

Si tratta di un flusso di lavoro tipico per le implementazioni di riferimento di Primetime DRM, caratterizzato sia dagli strumenti della riga di comando che dal server licenze:

1. Creare un criterio DRM utilizzando lo strumento della riga di comando Criterio.
1. Crittografare il contenuto utilizzando lo strumento della riga di comando Packager.
1. Distribuire il server licenze per le implementazioni di riferimento.
1. Carica un lettore video su un server web.
1. Utilizza il lettore video caricato per acquisire una licenza e riprodurre i contenuti crittografati.

Poiché questo flusso di lavoro tipico utilizza sia gli strumenti della riga di comando che il server licenze, è necessario installare e configurare entrambi i componenti prima di procedere.
