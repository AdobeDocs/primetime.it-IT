---
description: Quando si reimposta un'istanza MediaPlayer, viene restituito al relativo stato IDLE non inizializzato come definito in MediaPlayerState.
title: Reimpostare o riutilizzare un'istanza MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---


# Reimpostare, riutilizzare o rimuovere un&#39;istanza di MediaPlayer {#reset-or-reuse-a-mediaplayer-instance}

È possibile reimpostare, riutilizzare o rilasciare un&#39;istanza MediaPlayer non più necessaria.

Quando si reimposta un&#39;istanza MediaPlayer, viene restituito al relativo stato IDLE non inizializzato come definito in MediaPlayerState.

Questa operazione è utile nei casi seguenti:

* Desideri riutilizzare un&#39;istanza `MediaPlayer` ma devi caricare una nuova `MediaResource` (contenuto video) e sostituire l&#39;istanza precedente.

   La reimpostazione consente di riutilizzare l’istanza `MediaPlayer` senza sovraccaricare le risorse rilasciate, ricreare l’ `MediaPlayer` e riallocare le risorse.

* Quando il `MediaPlayer` si trova in uno stato ERROR e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l&#39;unico modo per recuperare dallo stato ERROR.

1. Invoca `reset` per restituire l&#39;istanza `MediaPlayer` al suo stato non inizializzato:

   ```java
   void reset() throws IllegalStateException; 
   ```

1. Utilizza `MediaPlayer.replaceCurrentResource` per caricare un altro `MediaResource`.

   >[!TIP]
   >
   >Per cancellare un errore, carica lo stesso `MediaResource`.

1. Quando ricevi il callback dell&#39;evento `STATUS_CHANGED` con stato PREPARED, avvia la riproduzione.

## Rilascia un&#39;istanza e risorse MediaPlayer{#release-a-mediaplayer-instance-and-resources}

È necessario rilasciare un&#39;istanza e risorse MediaPlayer quando non è più necessario MediaResource.

Quando si rilascia un oggetto `MediaPlayer`, le risorse hardware sottostanti associate a questo oggetto `MediaPlayer` vengono deallocate.

Ecco alcuni motivi per rilasciare un MediaPlayer:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Lasciare un oggetto `MediaPlayer` non necessario può comportare un consumo continuo di batterie per i dispositivi mobili.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

1. Rilascia il `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

Una volta rilasciata l’istanza `MediaPlayer`, non puoi più utilizzarla. Se dopo il rilascio viene chiamato un metodo dell&#39;interfaccia `MediaPlayer` , viene lanciato un `IllegalStateException` .