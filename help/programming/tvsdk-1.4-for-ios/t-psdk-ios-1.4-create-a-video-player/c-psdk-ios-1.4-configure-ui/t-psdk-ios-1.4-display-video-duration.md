---
description: Potete visualizzare la durata del contenuto attualmente attivo.
seo-description: Potete visualizzare la durata del contenuto attualmente attivo.
seo-title: Visualizzare la durata del video
title: Visualizzare la durata del video
uuid: 02042070-9c55-4cbb-9dc1-49987451eb8f
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Visualizzare la durata del video {#display-the-duration-of-the-video}

Potete visualizzare la durata del contenuto attualmente attivo.

Implementate una visualizzazione della durata del video utilizzando il seguente codice di esempio:

    La proprietà &quot;PTMediaPlayer&quot;, [searchRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange), contiene l&#39;intervallo di finestre ricercabili corrente:
    
    * Per VOD, questo intervallo corrisponde all&#39;intero intervallo di contenuti VOD, inclusi gli annunci.
    * Per live/lineari, questo intervallo rappresenta la finestra ricercabile.
    
    Per ulteriori informazioni sull&#39;API, consultate [TVSDK 1.4 for iOS API Reference](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
