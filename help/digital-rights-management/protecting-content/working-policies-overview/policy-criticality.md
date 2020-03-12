---
seo-title: Criticità politica DRM
title: Criticità politica DRM
uuid: ddc03142-7acb-4a9f-a367-e34cfc5e78ba
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Criticità politica DRM{#drm-policy-criticality}

Se prevedete di applicare nuove regole di utilizzo in un criterio DRM, e se prevedete di utilizzare questo criterio DRM nel contenuto creato per i server licenze meno recenti (e quindi non interpreta correttamente le nuove regole di utilizzo), potrebbe essere necessario specificare il funzionamento dei server licenze meno recenti. Per impostazione predefinita, la criticità del criterio DRM è impostata su `true`.

Questa impostazione indica che il server licenze deve elaborare tutte le parti del criterio DRM prima di poter generare una licenza che utilizza il criterio DRM specificato. Se la criticità del criterio DRM è impostata su `false`, un server licenze precedente potrebbe ignorare le parti del criterio DRM che non è in grado di interpretare correttamente. Di conseguenza, tutte le licenze generate dal server non includono nuove regole di utilizzo.

I server DRM Primetime che supportano la versione 2.0.2 dell&#39;SDK o versioni successive accettano l&#39;impostazione di criticità dei criteri DRM.
