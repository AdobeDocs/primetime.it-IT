---
title: Caricamento sicuro degli annunci tramite HTTPS
description: Caricamento sicuro degli annunci tramite HTTPS
copied-description: true
exl-id: 752d9a35-2faa-4953-8357-e2aff445d3c7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---

# Caricamento sicuro degli annunci tramite HTTPS {#secure-ad-loading-over-https}

Adobe Primetime fornisce un’opzione per richiedere la prima chiamata al server di annunci Primetime e alle chiamate relative a CRS tramite HTTPS.

La funzione non è attivata per impostazione predefinita. Utilizza quanto segue per abilitare il caricamento sicuro degli annunci.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
