---
description: È possibile attivare o disattivare le funzionalità senza passare attraverso il codice utilizzando la fabbrica del manager.
seo-description: È possibile attivare o disattivare le funzionalità senza passare attraverso il codice utilizzando la fabbrica del manager.
seo-title: Attivazione o disattivazione delle funzioni tramite ManagerFactory
title: Attivazione o disattivazione delle funzioni tramite ManagerFactory
uuid: 385c2707-95f7-4628-8d25-67731151cb6a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Attivazione o disattivazione delle funzioni tramite ManagerFactory{#turning-features-on-or-off-using-managerfactory}

È possibile attivare o disattivare le funzionalità senza passare attraverso il codice utilizzando la fabbrica del manager.

L’argomento enablement nell’esempio seguente determina se la funzione viene utilizzata o meno. Se è false, viene creato il gestore di funzioni, ma fornisce al lettore solo la funzionalità predefinita, come se il manager di funzioni non fosse stato creato. Se è vero, viene creato il gestore di funzioni, la funzione viene attivata e il lettore multimediale accetta l&#39;input dal file di configurazione.

Ad esempio, nel `com.adobe.primetime.reference.ui.player.PlayerFragment.java` file:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**Documentazione** API: [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)