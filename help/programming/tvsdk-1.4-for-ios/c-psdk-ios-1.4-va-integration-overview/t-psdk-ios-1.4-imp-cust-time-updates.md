---
description: In alcune implementazioni di analisi, l'applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localTime di TVSDK. Ad esempio, durante la riproduzione di un flusso lineare, è possibile fornire la testina di riproduzione di ogni programma in relazione al tempo di inizio.
seo-description: In alcune implementazioni di analisi, l'applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localTime di TVSDK. Ad esempio, durante la riproduzione di un flusso lineare, è possibile fornire la testina di riproduzione di ogni programma in relazione al tempo di inizio.
seo-title: Implementazione di aggiornamenti temporali personalizzati
title: Implementazione di aggiornamenti temporali personalizzati
uuid: 303303eb-c371-4766-a1ee-806ba75b4e01
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Implementa aggiornamenti temporali personalizzati{#implement-custom-time-updates}

In alcune implementazioni di analisi, l&#39;applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localTime di TVSDK. Ad esempio, durante la riproduzione di un flusso lineare, è possibile fornire la testina di riproduzione di ogni programma in relazione al tempo di inizio.

>[!TIP]
>
>Ignorare questo metodo solo se si desidera fornire una posizione dell&#39;indicatore di riproduzione diversa dalla posizione predefinita.

1. Per ignorare la posizione predefinita dell&#39;indicatore di riproduzione:

   ```
   vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
       NSInteger random = arc4random() % 500;  
       return CMTimeMakeWithSeconds(random, 1); 
   };
   ```

   >[!IMPORTANT]
   >
   >In questo esempio di codice, 500 è solo un valore di esempio. È necessario utilizzare un valore diverso per la posizione personalizzata dell&#39;indicatore di riproduzione.

