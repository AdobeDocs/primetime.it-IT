---
description: In alcune implementazioni di Analytics, l’applicazione client potrebbe voler fornire una posizione della testina di riproduzione diversa da quella riportata dal valore localTime dell’SDK. Ad esempio, durante una riproduzione lineare dello streaming, è possibile fornire la testina di riproduzione di ciascun programma relativamente al suo tempo di avvio.
title: Implementare aggiornamenti dell’ora personalizzati
exl-id: 85ec4744-541f-451f-95a3-063dd1151635
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Implementare aggiornamenti dell’ora personalizzati{#implement-custom-time-updates}

In alcune implementazioni di Analytics, l’applicazione client potrebbe voler fornire una posizione della testina di riproduzione diversa da quella riportata dal valore localTime dell’SDK. Ad esempio, durante una riproduzione lineare dello streaming, è possibile fornire la testina di riproduzione di ciascun programma relativamente al suo tempo di avvio.

>[!TIP]
>
>Ignora questo metodo solo se desideri fornire una posizione della testina di riproduzione diversa dalla posizione predefinita.

1. Per ignorare la posizione predefinita della testina di riproduzione:

   ```
   vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
       NSInteger random = arc4random() % 500;  
       return CMTimeMakeWithSeconds(random, 1); 
   };
   ```

   >[!IMPORTANT]
   >
   >In questo esempio di codice, 500 è solo un valore di esempio. Devi utilizzare un valore diverso per la posizione personalizzata della testina di riproduzione.
