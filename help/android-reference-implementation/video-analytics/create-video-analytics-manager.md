---
description: Creare Video Analytics Manager
title: Creare Video Analytics Manager
exl-id: 8d2bbb39-10e2-43e8-8ed3-bc376b3f3cc8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Creare Video Analytics Manager {#create-the-video-analytics-manager}

Una nuova classe Manager ( `VAManager`) è stato aggiunto all&#39;implementazione di riferimento Android. `VAManager` crea ed elimina semplicemente un&#39;istanza del `VideoHeartbeat` classe. L’implementazione di riferimento crea un’ `VAManager` istanza quando un nuovo `MediaPlayer` viene creata ed elimina tale istanza quando `MediaPlayer` viene distrutto. Implementato in `PlayerFragment.java`.

## Per creare un nuovo Video Analytics Manager

```java
VAManager vaManager = ManagerFactory.getVAManager(true, config, mediaPlayer);  
vaManager.createVAProvider(getActivity().getApplicationContext()); 
```

La variabile di configurazione è un’implementazione concreta di `IVAConfig` e contiene il runtime `VideoHeartbeat` configurazioni.

>[!NOTE]
>
>Se l’applicazione Android non è configurata con un account Adobe Analytics, i dati di tracciamento video non verranno generati, anche se un’istanza di `VAManager` viene creato e attivato.
