---
description: TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel manifesto del contenuto.
title: Iscriviti ai tag personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---


# Iscriviti ai tag personalizzati{#subscribe-to-custom-tags}

TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel manifesto del contenuto.

Prima di avviare la riproduzione, è necessario abbonarsi ai tag.
Per ricevere notifiche sui tag personalizzati nei manifesti HLS:

Imposta globalmente i nomi dei tag di annunci personalizzati passando una matrice che contiene i tag personalizzati a `setSubscribedTags` in `MediaPlayerItemConfig`.

>[!IMPORTANT]
>
>È necessario includere il prefisso `#` quando si lavora con i flussi HLS.

Ad esempio:

```java
String[] array = new String[3]; 
array[0] = "#EXT-X-ASSET"; 
array[1] = "#EXT-X-BLACKOUT"; 
array[2] = "#EXT-OATCLS-SCTE35"; 
MediaPlayerItemConfig.setSubscribedTags(array);
```

