---
description: È possibile attivare o disattivare le funzionalità senza passare attraverso il codice utilizzando la fabbrica del manager.
title: Attivazione o disattivazione delle feature mediante ManagerFactory
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Attivazione o disattivazione delle feature mediante ManagerFactory{#turning-features-on-or-off-using-managerfactory}

È possibile attivare o disattivare le funzionalità senza passare attraverso il codice utilizzando la fabbrica del manager.

L&#39;argomento di abilitazione nell&#39;esempio seguente determina se la funzione viene utilizzata o meno. Se è false, viene creato il gestore delle funzioni, ma fornisce solo la funzionalità predefinita al lettore, come se il gestore delle funzioni non fosse stato creato. Se è true, viene creato il gestore delle funzioni, la funzione viene abilitata e il lettore multimediale accetta l’input dal file di configurazione.

Ad esempio, nel `com.adobe.primetime.reference.ui.player.PlayerFragment.java` file:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);
```

**Documentazione API**: [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)
