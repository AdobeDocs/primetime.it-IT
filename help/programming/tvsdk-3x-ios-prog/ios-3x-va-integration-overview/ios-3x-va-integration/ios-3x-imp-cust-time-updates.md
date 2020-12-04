---
description: In alcune implementazioni di analisi, l'applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localTime di TVSDK. Ad esempio, durante la riproduzione di un flusso lineare, è possibile fornire la testina di riproduzione di ogni programma in relazione al tempo di inizio.
seo-description: In alcune implementazioni di analisi, l'applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localTime di TVSDK. Ad esempio, durante la riproduzione di un flusso lineare, è possibile fornire la testina di riproduzione di ogni programma in relazione al tempo di inizio.
seo-title: Implementazione di aggiornamenti temporali personalizzati
title: Implementazione di aggiornamenti temporali personalizzati
uuid: 174937ca-3c26-4385-a298-8a01fc93ea20
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Implementare gli aggiornamenti temporali personalizzati {#implement-custom-time-updates}

In alcune implementazioni di analisi, l&#39;applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localTime di TVSDK. Ad esempio, durante la riproduzione di un flusso lineare, è possibile fornire la testina di riproduzione di ogni programma in relazione al tempo di inizio.

>[!TIP]
>
>Ignorare questo metodo solo se si desidera fornire una posizione dell&#39;indicatore di riproduzione diversa dalla posizione predefinita.

Per ignorare la posizione predefinita dell&#39;indicatore di riproduzione:

```
vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
    NSInteger random = arc4random() % 500;  
    return CMTimeMakeWithSeconds(random, 1); 
};
```

>[!IMPORTANT]
>
>In questo esempio di codice, 500 è solo un valore di esempio. È necessario utilizzare un valore diverso per la posizione personalizzata dell&#39;indicatore di riproduzione.