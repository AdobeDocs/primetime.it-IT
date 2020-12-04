---
description: In alcune implementazioni di analisi, l'applicazione client potrebbe voler fornire una posizione di playhead diversa da quella segnalata dal valore localeTime di TVSDK. Ad esempio, durante la riproduzione di un flusso LINEAR, è possibile fornire la testina di riproduzione di ogni programma in relazione all'ora di inizio.
seo-description: In alcune implementazioni di analisi, l'applicazione client potrebbe voler fornire una posizione di playhead diversa da quella segnalata dal valore localeTime di TVSDK. Ad esempio, durante la riproduzione di un flusso LINEAR, è possibile fornire la testina di riproduzione di ogni programma in relazione all'ora di inizio.
seo-title: Implementazione di aggiornamenti temporali personalizzati
title: Implementazione di aggiornamenti temporali personalizzati
uuid: 2b46eca9-3815-4c44-ab5e-21678c35f410
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Implementa aggiornamenti temporali personalizzati{#implement-custom-time-updates}

In alcune implementazioni di analisi, l&#39;applicazione client potrebbe voler fornire una posizione di playhead diversa da quella segnalata dal valore localeTime di TVSDK. Ad esempio, durante la riproduzione di un flusso LINEAR, è possibile fornire la testina di riproduzione di ogni programma in relazione all&#39;ora di inizio.

>[!TIP]
>
>Ignora questo metodo solo se si desidera fornire una posizione diversa dell&#39;indicatore di riproduzione rispetto alla posizione predefinita.

1. Per ignorare la posizione predefinita dell&#39;indicatore di riproduzione:

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
   >I valori in questo frammento di codice sono solo esempi. È necessario utilizzare valori diversi per la posizione personalizzata dell&#39;indicatore di riproduzione.

