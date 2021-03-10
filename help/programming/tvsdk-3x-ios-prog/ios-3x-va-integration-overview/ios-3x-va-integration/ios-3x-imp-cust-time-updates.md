---
description: In alcune implementazioni di Analytics, l'applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localTime di TVSDK. Ad esempio, durante la riproduzione di un flusso lineare, la testina di riproduzione di ogni programma può essere fornita in base al tempo di inizio.
title: Implementare aggiornamenti temporali personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Implementare aggiornamenti ora personalizzati {#implement-custom-time-updates}

In alcune implementazioni di Analytics, l&#39;applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localTime di TVSDK. Ad esempio, durante la riproduzione di un flusso lineare, la testina di riproduzione di ogni programma può essere fornita in base al tempo di inizio.

>[!TIP]
>
>Ignorare questo metodo solo se si desidera fornire una posizione diversa da quella predefinita.

Per sovrascrivere la posizione predefinita della testina di riproduzione:

```
vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
    NSInteger random = arc4random() % 500;  
    return CMTimeMakeWithSeconds(random, 1); 
};
```

>[!IMPORTANT]
>
>In questo esempio di codice, 500 è solo un valore di esempio. È necessario utilizzare un valore diverso per la posizione personalizzata della testina di riproduzione.