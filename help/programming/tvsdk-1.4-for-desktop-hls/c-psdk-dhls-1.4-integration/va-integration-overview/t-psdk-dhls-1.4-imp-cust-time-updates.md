---
description: In alcune implementazioni di analytics, l'applicazione client può voler fornire una posizione di playhead diversa da quella indicata dal valore localeTime TVSDK. Ad esempio, durante la riproduzione di un flusso LINEAR, la testina di riproduzione di ogni programma può essere fornita in base all'ora di inizio.
title: Implementare aggiornamenti temporali personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Implementa aggiornamenti temporali personalizzati{#implement-custom-time-updates}

In alcune implementazioni di analytics, l&#39;applicazione client può voler fornire una posizione di playhead diversa da quella indicata dal valore localeTime TVSDK. Ad esempio, durante la riproduzione di un flusso LINEAR, la testina di riproduzione di ogni programma può essere fornita in base all&#39;ora di inizio.

>[!TIP]
>
>Ignorare questo metodo solo se si desidera fornire una posizione diversa della testina di riproduzione rispetto alla posizione predefinita.

1. Per sovrascrivere la posizione predefinita della testina di riproduzione:

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
   >I valori in questo frammento di codice sono solo esempi. È necessario utilizzare valori diversi per la posizione personalizzata della testina di riproduzione.

