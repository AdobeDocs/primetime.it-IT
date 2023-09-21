---
title: Criticità delle politiche DRM
description: Criticità delle politiche DRM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Criticità delle politiche DRM{#drm-policy-criticality}

Se si prevede di applicare nuove regole di utilizzo in un criterio DRM e si prevede di utilizzare questo criterio DRM nel contenuto che è stato creato per i server licenze meno recenti (e quindi non interpreta correttamente le nuove regole di utilizzo), potrebbe essere necessario specificare il comportamento dei server licenze meno recenti. Per impostazione predefinita, la criticità dei criteri DRM è impostata su `true`.

Questa impostazione indica che il server licenze deve elaborare tutte le parti del criterio DRM prima di poter generare una licenza che utilizzi il criterio DRM specificato. Se la criticità della policy DRM è impostata su `false`, un server licenze meno recente può ignorare le parti del criterio DRM che non è in grado di interpretare correttamente. Pertanto, le licenze generate dal server non includono nuove regole di utilizzo.

I server DRM di Primetime che supportano la versione 2.0.2 dell’SDK o successiva accettano l’impostazione di criticità dei criteri DRM.
