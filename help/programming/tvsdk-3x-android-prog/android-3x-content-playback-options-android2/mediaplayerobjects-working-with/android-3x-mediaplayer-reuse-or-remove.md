---
description: È possibile reimpostare, riutilizzare o rilasciare un'istanza MediaPlayer non più necessaria.
title: Riutilizzare o rimuovere un'istanza MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# Riutilizzare o rimuovere un&#39;istanza MediaPlayer {#reuse-or-remove-a-mediaplayer-instance}

È possibile reimpostare, riutilizzare o rilasciare un&#39;istanza MediaPlayer non più necessaria.

## Reimpostare o riutilizzare un&#39;istanza di MediaPlayer {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

Quando si reimposta un&#39;istanza `MediaPlayer`, viene restituito al relativo stato IDLE non inizializzato come definito in `MediaPlayerStatus`.

Questa operazione è utile nei casi seguenti:

* Desideri riutilizzare un&#39;istanza `MediaPlayer` ma devi caricare una nuova `MediaResource` (contenuto video) e sostituire l&#39;istanza precedente.

   La reimpostazione consente di riutilizzare l’istanza `MediaPlayer` senza sovraccaricare le risorse rilasciate, ricreare l’ `MediaPlayer` e riallocare le risorse.

* Quando il `MediaPlayer` è nello stato ERROR e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l&#39;unico modo per recuperare dallo stato ERROR.

   1. Invoca `reset` per restituire l&#39;istanza `MediaPlayer` al suo stato non inizializzato:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Utilizza `MediaPlayer.replaceCurrentResource()` per caricare un altro `MediaResource`.

      >[!NOTE]
      >
      >Per cancellare un errore, carica lo stesso `MediaResource`.

   1. Quando ricevi il callback dell&#39;evento `STATUS_CHANGED` con stato `PREPARED`, avvia la riproduzione.

## Rilascia un&#39;istanza e risorse MediaPlayer {#section_13A0914AFF784943ABC343F7EB249C4E}

Rilasciare un&#39;istanza e risorse `MediaPlayer` quando non è più necessario `MediaResource`.

Quando si rilascia un oggetto `MediaPlayer`, le risorse hardware sottostanti associate a questo oggetto `MediaPlayer` vengono deallocate.

Di seguito sono riportati alcuni motivi per rilasciare un `MediaPlayer`:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Se si lascia un oggetto `MediaPlayer` non necessario, l&#39;istanza può comportare un consumo continuo di batterie per i dispositivi mobili.
* Se sono presenti più istanze
Se un dispositivo non supporta lo stesso codec video, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

* Rilascia il `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >Una volta rilasciata l’istanza `MediaPlayer`, non puoi più utilizzarla. Se dopo il rilascio viene chiamato un metodo dell&#39;interfaccia `MediaPlayer` , viene lanciato un `MediaPlayerException` .