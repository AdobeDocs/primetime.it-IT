---
description: È possibile attivare o disattivare le funzionalità senza passare attraverso il codice utilizzando la fabbrica del manager.
title: Attivazione o disattivazione delle feature mediante ManagerFactory
exl-id: 4e288a6e-80e5-43c1-aba2-374723dd9957
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
