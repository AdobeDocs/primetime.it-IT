---
description: In alcune implementazioni di analisi, l'applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localTime di TVSDK del browser.
seo-description: In alcune implementazioni di analisi, l'applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localTime di TVSDK del browser.
seo-title: Implementazione di aggiornamenti temporali personalizzati
title: Implementazione di aggiornamenti temporali personalizzati
uuid: 26a0592c-a47b-4d65-b984-5e51533dcddc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Implementa aggiornamenti temporali personalizzati{#implement-custom-time-updates}

In alcune implementazioni di analisi, l&#39;applicazione client potrebbe voler fornire una posizione di playhead diversa da quella indicata dal valore localTime di TVSDK del browser.

Ad esempio, durante la riproduzione di un flusso lineare, è possibile fornire la testina di riproduzione di ogni programma in relazione al tempo di inizio.

>[!TIP]
>
>Ignora questo metodo solo se si desidera fornire una posizione dell&#39;indicatore di riproduzione diversa dalla posizione predefinita.

Per ignorare la posizione predefinita dell&#39;indicatore di riproduzione:

```js
vaMetadata.currentTimeUpdateBlock = function() { 
       return playerPositionInSeconds; 
}; 
```

>[!IMPORTANT]
>
>I valori in questo frammento di codice sono solo esempi. È necessario utilizzare valori diversi per la posizione personalizzata dell&#39;indicatore di riproduzione.

