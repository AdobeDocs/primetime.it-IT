---
description: È possibile attivare o disattivare le funzionalità senza passare attraverso il codice utilizzando la fabbrica di gestione.
title: Attivazione o disattivazione delle funzioni con ManagerFactory
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Attivazione o disattivazione delle funzioni utilizzando ManagerFactory{#turning-features-on-or-off-using-managerfactory}

È possibile attivare o disattivare le funzionalità senza passare attraverso il codice utilizzando la fabbrica di gestione.

L’argomento di abilitazione nell’esempio seguente determina se la funzione viene utilizzata o meno. Se è false, viene creato il gestore di funzioni, ma fornisce solo la funzionalità predefinita al lettore, come se il gestore di funzioni non fosse stato creato. Se è vero, viene creato il gestore di funzioni, la funzione viene abilitata e il lettore multimediale accetta l&#39;input dal file di configurazione.

Ad esempio, nel file `com.adobe.primetime.reference.ui.player.PlayerFragment.java` :

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**Documentazione** API:  [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)