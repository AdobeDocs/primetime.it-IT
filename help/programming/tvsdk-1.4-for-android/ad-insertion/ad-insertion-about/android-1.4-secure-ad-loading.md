---
description: 'null'
seo-description: 'null'
seo-title: Protezione del caricamento di annunci tramite HTTPS
title: Protezione del caricamento di annunci tramite HTTPS
uuid: 0d680fef-a372-4157-a89b-d9f10003c768
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 0%

---


# Caricamento annunci protetti tramite HTTPS{#secure-ad-loading-over-https}

 Adobe Primetime fornisce un&#39;opzione per richiedere la prima chiamata al server per gli annunci Primetime e alle chiamate relative ai CRS attraverso il protocollo HTTPS.

Per impostazione predefinita, la funzione non è abilitata. Utilizzate quanto segue per abilitare il caricamento sicuro degli annunci.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

