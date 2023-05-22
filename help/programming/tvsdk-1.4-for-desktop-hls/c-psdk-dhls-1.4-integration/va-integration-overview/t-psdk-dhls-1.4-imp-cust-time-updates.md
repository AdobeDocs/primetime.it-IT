---
description: In alcune implementazioni di Analytics, l’applicazione client potrebbe voler fornire una posizione della testina di riproduzione diversa da quella riportata dal valore localTime di TVSDK. Ad esempio, durante una riproduzione LINEAR in streaming, è possibile fornire la testina di riproduzione di ciascun programma relativamente al suo tempo di avvio.
title: Implementare aggiornamenti dell’ora personalizzati
exl-id: be0f2684-6a17-4d99-8875-7f404ce8a656
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Implementare aggiornamenti dell’ora personalizzati{#implement-custom-time-updates}

In alcune implementazioni di Analytics, l’applicazione client potrebbe voler fornire una posizione della testina di riproduzione diversa da quella riportata dal valore localTime di TVSDK. Ad esempio, durante una riproduzione LINEAR in streaming, è possibile fornire la testina di riproduzione di ciascun programma relativamente al suo tempo di avvio.

>[!TIP]
>
>Ignora questo metodo solo se desideri fornire una posizione della testina di riproduzione diversa da quella predefinita.

1. Per ignorare la posizione predefinita della testina di riproduzione:

   ```
   vaMetadata.currentTimeUpdateBlock = function():Number { 
      if (currentTime == 0) { 
          currentTime = getTimer(); 
      } 
      return ((getTimer() - currentTime) / 1000 + 1000); 
   }
   ```

   >[!IMPORTANT]
   >
   >I valori in questo frammento di codice sono solo esempi. Devi utilizzare valori diversi per la posizione personalizzata della testina di riproduzione.
