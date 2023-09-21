---
title: Flusso di lavoro tipico
description: Flusso di lavoro tipico
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Flusso di lavoro tipico{#typical-workflow}

Si tratta di un flusso di lavoro tipico per le implementazioni di riferimento di Primetime DRM, caratterizzato sia dagli strumenti della riga di comando che dal server licenze:

1. Creare un criterio DRM utilizzando lo strumento della riga di comando Criterio.
1. Crittografare il contenuto utilizzando lo strumento della riga di comando Packager.
1. Distribuisci il server licenze per le implementazioni di riferimento.
1. Carica un lettore video su un server web.
1. Utilizza il lettore video caricato per acquisire una licenza e riprodurre i contenuti crittografati.

Poiché questo flusso di lavoro tipico utilizza sia gli strumenti della riga di comando che il server licenze, è necessario installare e configurare entrambi i componenti prima di procedere.
