---
title: Caricamento dell'annuncio protetto su HTTPS
description: Caricamento dell'annuncio protetto su HTTPS
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# Caricamento dell&#39;annuncio protetto su HTTPS {#secure-ad-loading-over-https}

Adobe Primetime fornisce un&#39;opzione per richiedere la prima chiamata al server ad Primetime e alle chiamate relative a CRS su HTTPS.

La funzione non è abilitata per impostazione predefinita. Utilizza quanto segue per abilitare il caricamento sicuro degli annunci.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

