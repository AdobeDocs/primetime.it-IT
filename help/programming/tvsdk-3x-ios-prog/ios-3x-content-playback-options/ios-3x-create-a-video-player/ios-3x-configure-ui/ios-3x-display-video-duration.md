---
description: Puoi visualizzare la durata del contenuto attualmente attivo.
title: Visualizza la durata del video
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Visualizza la durata del video {#display-the-duration-of-the-video}

Puoi visualizzare la durata del contenuto attualmente attivo.

Implementa una visualizzazione della durata video utilizzando il seguente codice di esempio:

Il `PTMediaPlayer` proprietà, [seekableRange](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html#//api/name/seekableRange), contiene l’intervallo di finestre attualmente ricercabili:

* Per VOD, questo intervallo corrisponde all’intero intervallo di contenuti VOD, inclusi gli annunci.
* Per live/linear, questo intervallo rappresenta la finestra ricercabile.

Per ulteriori informazioni sull’API, consulta [Riferimento API di TVSDK 3.4 per iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v3/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
