---
title: Caricamento sicuro degli annunci tramite HTTPS
description: Caricamento sicuro degli annunci tramite HTTPS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Caricamento sicuro degli annunci tramite HTTPS{#secure-ad-loading-over-https}

Adobe Primetime fornisce un’opzione per richiedere la prima chiamata al server di annunci Primetime e alle chiamate relative a CRS tramite HTTPS.

La funzione non è attivata per impostazione predefinita. Utilizza quanto segue per abilitare il caricamento sicuro degli annunci.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
