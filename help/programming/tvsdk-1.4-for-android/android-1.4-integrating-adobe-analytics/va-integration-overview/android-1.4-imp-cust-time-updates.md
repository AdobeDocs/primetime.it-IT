---
description: In alcune implementazioni di analisi, l'applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localeTime di TVSDK. Ad esempio, durante la riproduzione di un flusso lineare, è possibile fornire la testina di riproduzione di ogni programma in relazione al tempo di inizio.
seo-description: In alcune implementazioni di analisi, l'applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localeTime di TVSDK. Ad esempio, durante la riproduzione di un flusso lineare, è possibile fornire la testina di riproduzione di ogni programma in relazione al tempo di inizio.
seo-title: Implementazione di aggiornamenti temporali personalizzati
title: Implementazione di aggiornamenti temporali personalizzati
uuid: 7f5d46e5-eab6-4bdc-b015-ae27ddb609ce
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Implementare gli aggiornamenti temporali personalizzati {#implement-custom-time-updates}

In alcune implementazioni di analisi, l&#39;applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localeTime di TVSDK. Ad esempio, durante la riproduzione di un flusso lineare, è possibile fornire la testina di riproduzione di ogni programma in relazione al tempo di inizio.

>[!TIP]
>
>Ignora questo metodo solo se si desidera fornire una posizione dell&#39;indicatore di riproduzione diversa dalla posizione predefinita.

Per ignorare la posizione predefinita dell&#39;indicatore di riproduzione:

```java
vaMetadata.setCurrentTimeUpdateBlock(new VideoAnalyticsMetadata.CurrentTimeUpdateBlock() { 
    @Override 
    public long call() { 
        long range = 500L; 
        Random r = new Random() 
        return (long)(r.nextDouble()*range); 
    } 
});
```

>[!IMPORTANT]
>
>I valori in questo frammento di codice sono solo esempi. È necessario utilizzare valori diversi per la posizione personalizzata dell&#39;indicatore di riproduzione.