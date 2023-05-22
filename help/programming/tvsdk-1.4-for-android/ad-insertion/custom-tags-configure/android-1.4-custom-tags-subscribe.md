---
description: TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel manifesto del contenuto.
title: Iscriviti a tag personalizzati
exl-id: 7f1f86ca-eeba-43c3-ac2a-c493d05ad73a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Iscriviti a tag personalizzati{#subscribe-to-custom-tags}

TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel manifesto del contenuto.

Prima di avviare la riproduzione, è necessario iscriversi ai tag.
Per ricevere notifiche sui tag personalizzati nei manifesti HLS:

Imposta i nomi dei tag personalizzati dell’annuncio a livello globale trasmettendo un array che contiene i tag personalizzati a `setSubscribedTags` in `MediaPlayerItemConfig`.

>[!IMPORTANT]
>
>Devi includere `#` prefisso quando si lavora con flussi HLS.

Ad esempio:

```java
String[] array = new String[3]; 
array[0] = "#EXT-X-ASSET"; 
array[1] = "#EXT-X-BLACKOUT"; 
array[2] = "#EXT-OATCLS-SCTE35"; 
MediaPlayerItemConfig.setSubscribedTags(array);
```
