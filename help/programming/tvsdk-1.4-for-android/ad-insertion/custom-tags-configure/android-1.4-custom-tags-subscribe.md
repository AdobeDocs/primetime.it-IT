---
description: TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.
seo-description: TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.
seo-title: Iscriviti ai tag personalizzati
title: Iscriviti ai tag personalizzati
uuid: fe8ba34d-66fc-43bb-b98e-659c1702d1e0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 1%

---


# Iscriviti a tag personalizzati{#subscribe-to-custom-tags}

TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.

Prima di avviare la riproduzione, è necessario effettuare la sottoscrizione ai tag.
Per ricevere notifiche sui tag personalizzati nei manifesti HLS:

Impostate i nomi dei tag degli annunci personalizzati a livello globale passando un array che contiene i tag personalizzati a `setSubscribedTags` in `MediaPlayerItemConfig`.

>[!IMPORTANT]
>
>È necessario includere il prefisso `#` quando si utilizzano i flussi HLS.

Ad esempio:

```java
String[] array = new String[3]; 
array[0] = "#EXT-X-ASSET"; 
array[1] = "#EXT-X-BLACKOUT"; 
array[2] = "#EXT-OATCLS-SCTE35"; 
MediaPlayerItemConfig.setSubscribedTags(array);
```

