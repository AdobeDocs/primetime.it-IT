---
description: In alcune implementazioni di Analytics, l'applicazione client potrebbe voler fornire una posizione di playhead diversa rispetto alla posizione segnalata dal valore localTime del browser TVSDK.
title: Implementare aggiornamenti temporali personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Implementa aggiornamenti temporali personalizzati{#implement-custom-time-updates}

In alcune implementazioni di Analytics, l&#39;applicazione client potrebbe voler fornire una posizione di playhead diversa rispetto alla posizione segnalata dal valore localTime del browser TVSDK.

Ad esempio, durante la riproduzione di un flusso lineare, la testina di riproduzione di ogni programma può essere fornita in base al tempo di inizio.

>[!TIP]
>
>Ignorare questo metodo solo se si desidera fornire una posizione diversa da quella predefinita.

Per sovrascrivere la posizione predefinita della testina di riproduzione:

```js
vaMetadata.currentTimeUpdateBlock = function() { 
       return playerPositionInSeconds; 
}; 
```

>[!IMPORTANT]
>
>I valori in questo frammento di codice sono solo esempi. È necessario utilizzare valori diversi per la posizione personalizzata della testina di riproduzione.

