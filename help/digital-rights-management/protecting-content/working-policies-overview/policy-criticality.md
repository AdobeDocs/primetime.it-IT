---
title: Criticità politica del DRM
description: Criticità politica del DRM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Criterio DRM{#drm-policy-criticality}

Se si prevede di applicare nuove regole di utilizzo in un criterio DRM e se si intende utilizzare questo criterio DRM in contenuti che sono stati assemblati per server licenze precedenti (e quindi non interpretano correttamente le nuove regole di utilizzo), potrebbe essere necessario specificare il comportamento dei server licenze precedenti. Per impostazione predefinita, la criticità dei criteri DRM è impostata su `true`.

Questa impostazione indica che il server licenze deve elaborare tutte le parti del criterio DRM prima di poter generare una licenza che utilizza il criterio DRM specificato. Se la criticità dei criteri DRM è impostata su `false`, un server licenze precedente può ignorare le parti del criterio DRM che non può interpretare correttamente. Pertanto, tutte le licenze generate dal server non includono nuove regole di utilizzo.

I server DRM di Primetime che supportano la versione 2.0.2 dell&#39;SDK o versioni successive accettano l&#39;impostazione di criticità dei criteri DRM.
