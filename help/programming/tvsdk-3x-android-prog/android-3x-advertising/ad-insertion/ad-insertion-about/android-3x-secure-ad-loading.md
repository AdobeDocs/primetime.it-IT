---
description: 'null'
seo-description: 'null'
seo-title: Protezione del caricamento di annunci tramite HTTPS
title: Protezione del caricamento di annunci tramite HTTPS
uuid: 18be77cc-c59b-4982-b8c1-e4451495edd2
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Protezione del caricamento di annunci tramite HTTPS {#secure-ad-loading-over-https}

Adobe Primetime fornisce un&#39;opzione per richiedere la prima chiamata al server per gli annunci Primetime e alle chiamate relative ai CRS attraverso il protocollo HTTPS.

Per impostazione predefinita, la funzione non è abilitata. Utilizzate quanto segue per abilitare il caricamento sicuro degli annunci.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
