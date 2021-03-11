---
title: Flusso di lavoro tipico
description: Flusso di lavoro tipico
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# Flusso di lavoro tipico{#typical-workflow}

Si tratta di un flusso di lavoro tipico delle implementazioni di riferimento DRM di Primetime che dispone sia degli strumenti della riga di comando che del server licenze:

1. Crea un criterio DRM utilizzando lo strumento a riga di comando Criterio.
1. Cifrare il contenuto utilizzando lo strumento a riga di comando Packager.
1. Distribuisci il server di licenze delle implementazioni di riferimento.
1. Carica un lettore video su un server web.
1. Utilizza il lettore video caricato per acquisire una licenza e riprodurre il contenuto crittografato.

Poiché questo flusso di lavoro tipico utilizza sia gli strumenti della riga di comando che il server licenze, è necessario installare e configurare entrambi i componenti prima di procedere.
