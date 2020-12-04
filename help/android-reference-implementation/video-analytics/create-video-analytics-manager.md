---
description: Creare Video Analytics Manager
seo-description: Creare Video Analytics Manager
seo-title: Creare Video Analytics Manager
title: Creare Video Analytics Manager
uuid: d72e1dfe-df70-47cc-9e00-bd09017d6127
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Creare Video Analytics Manager {#create-the-video-analytics-manager}

All&#39;implementazione di riferimento Android è stata aggiunta una nuova classe manager ( `VAManager`). `VAManager` crea e distrugge semplicemente un&#39;istanza della  `VideoHeartbeat` classe. L&#39;implementazione di riferimento crea un&#39;istanza `VAManager` quando viene creata una nuova istanza `MediaPlayer` e la distrugge quando la `MediaPlayer` viene distrutta. Questo è implementato in `PlayerFragment.java`.

## Per creare una nuova Gestione analisi video

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

La variabile config è un&#39;implementazione concreta di `IVAConfig` e contiene le configurazioni runtime `VideoHeartbeat`.

>[!NOTE]
>
>Se l’applicazione Android non è configurata con un account Adobe Analytics , i dati di tracciamento video non verranno generati, anche se viene creata e abilitata un’istanza di `VAManager`.

