---
description: Creare Video Analytics Manager
title: Creare Video Analytics Manager
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Creare Video Analytics Manager {#create-the-video-analytics-manager}

È stata aggiunta una nuova classe manager ( `VAManager`) all’implementazione di riferimento Android. `VAManager` crea e distrugge semplicemente un&#39;istanza della  `VideoHeartbeat` classe. L&#39;implementazione di riferimento crea un&#39;istanza `VAManager` quando viene creato un nuovo `MediaPlayer` e distrugge tale istanza quando il `MediaPlayer` viene distrutto. Questa è implementata in `PlayerFragment.java`.

## Per creare un nuovo Video Analytics Manager

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

La variabile di configurazione è un&#39;implementazione concreta di `IVAConfig` e contiene le configurazioni di runtime `VideoHeartbeat`.

>[!NOTE]
>
>Se l&#39;applicazione Android non è configurata con un account Adobe Analytics, i dati di tracciamento video non verranno generati, anche se viene creata e abilitata un&#39;istanza di `VAManager` .

