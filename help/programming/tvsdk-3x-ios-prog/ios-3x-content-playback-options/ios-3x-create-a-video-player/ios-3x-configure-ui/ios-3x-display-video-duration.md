---
description: Potete visualizzare la durata del contenuto attualmente attivo.
seo-description: Potete visualizzare la durata del contenuto attualmente attivo.
seo-title: Visualizzare la durata del video
title: Visualizzare la durata del video
uuid: 945f222d-80ba-4832-a06f-9bb8db6adbcb
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Visualizza la durata del video {#display-the-duration-of-the-video}

Potete visualizzare la durata del contenuto attualmente attivo.

Implementate una visualizzazione della durata del video utilizzando il seguente codice di esempio:

    La proprietà `PTMediaPlayer`, ` [searchRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange)`, contiene l&#39;intervallo di finestre ricercabili corrente:
    
    * Per VOD, questo intervallo è l&#39;intero intervallo di contenuti VOD, inclusi gli annunci.
    * Per live/lineari, questo intervallo rappresenta la finestra ricercabile.
    
    Per ulteriori informazioni sull&#39;API, consultate [TVSDK 3.4 for iOS API Reference](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
