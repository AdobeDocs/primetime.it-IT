---
description: 'null'
seo-description: 'null'
seo-title: Protezione del caricamento di annunci tramite HTTPS
title: Protezione del caricamento di annunci tramite HTTPS
uuid: 72ab94d3-ee0c-4f02-adf2-c186ae6aec26
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Protezione del caricamento di annunci tramite HTTPS {#secure-ad-loading-over-https}

Adobe Primetime fornisce un&#39;opzione per richiedere la prima chiamata al server per gli annunci Primetime e alle chiamate relative ai CRS attraverso il protocollo HTTPS.

Per impostazione predefinita, la funzione non è abilitata. Utilizzate quanto segue per abilitare il caricamento sicuro degli annunci.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```

