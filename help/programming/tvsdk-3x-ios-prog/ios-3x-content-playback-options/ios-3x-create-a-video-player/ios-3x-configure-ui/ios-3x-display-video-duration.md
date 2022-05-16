---
description: È possibile visualizzare la durata del contenuto attualmente attivo.
title: Visualizza la durata del video
exl-id: a41cb291-9355-44cf-80bb-9c3cf6628b81
source-git-commit: 85818281390b68522da2663496be025acf8f8675
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Visualizza la durata del video {#display-the-duration-of-the-video}

È possibile visualizzare la durata del contenuto attualmente attivo.

Implementa una visualizzazione a durata video utilizzando il seguente codice di esempio:

La `PTMediaPlayer` proprietà, [searchkableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange), contiene l&#39;intervallo di finestre ricercabili corrente:

* Per VOD, questo intervallo è l’intero intervallo di contenuti VOD, inclusi gli annunci.
* Per le immagini live/lineari, questo intervallo rappresenta la finestra ricercabile.

Per ulteriori informazioni sull’API, consulta [Guida di riferimento per l’API TVSDK 3.4 per iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
