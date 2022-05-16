---
description: È possibile visualizzare la durata del contenuto attualmente attivo.
title: Visualizza la durata del video
exl-id: 4e31d784-4d16-470b-8317-11be32a55c2f
source-git-commit: 0019a95fa9ca6d21249533d559ce844897ab67cf
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

Per ulteriori informazioni sull’API, consulta [Guida di riferimento per l’API TVSDK 1.4 per iOS](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/index.html)

<!--<a id="example_A153BE3AC03F43C6BF3A156316A08CD3"></a>-->

```
CMTimeRange seekableRange = self.player.seekableRange;  
if (CMTIMERANGE_IS_VALID(seekableRange)) { 
    double start = CMTimeGetSeconds(seekableRange.start);  
    double duration = CMTimeGetSeconds(seekableRange.duration); 
}
```
