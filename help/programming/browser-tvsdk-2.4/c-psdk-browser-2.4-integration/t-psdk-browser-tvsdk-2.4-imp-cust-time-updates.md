---
description: In alcune implementazioni di Analytics, l’applicazione client potrebbe voler fornire una posizione della testina di riproduzione diversa da quella riportata dal valore localTime di TVSDK del browser.
title: Implementare aggiornamenti dell’ora personalizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Implementare aggiornamenti dell’ora personalizzati{#implement-custom-time-updates}

In alcune implementazioni di Analytics, l’applicazione client potrebbe voler fornire una posizione della testina di riproduzione diversa da quella riportata dal valore localTime di TVSDK del browser.

Ad esempio, durante una riproduzione lineare dello streaming, è possibile fornire la testina di riproduzione di ciascun programma relativamente al suo tempo di avvio.

>[!TIP]
>
>Ignora questo metodo solo se desideri fornire una posizione della testina di riproduzione diversa dalla posizione predefinita.

Per ignorare la posizione predefinita della testina di riproduzione:

```js
vaMetadata.currentTimeUpdateBlock = function() { 
       return playerPositionInSeconds; 
}; 
```

>[!IMPORTANT]
>
>I valori in questo frammento di codice sono solo esempi. Devi utilizzare valori diversi per la posizione personalizzata della testina di riproduzione.
