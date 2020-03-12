---
description: Quando reimpostate un’istanza di MediaPlayer, viene riportato al relativo stato IDLE non inizializzato, come definito in MediaPlayerState.
seo-description: Quando reimpostate un’istanza di MediaPlayer, viene riportato al relativo stato IDLE non inizializzato, come definito in MediaPlayerState.
seo-title: Reimpostare o riutilizzare un'istanza di MediaPlayer
title: Reimpostare o riutilizzare un'istanza di MediaPlayer
uuid: 72cc4511-8ab0-44e5-b93c-b36f0321bba8
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Reimpostare, riutilizzare o rimuovere un’istanza di MediaPlayer {#reset-or-reuse-a-mediaplayer-instance}

È possibile ripristinare, riutilizzare o rilasciare un&#39;istanza di MediaPlayer non più necessaria.

Quando reimpostate un’istanza di MediaPlayer, viene riportato al relativo stato IDLE non inizializzato, come definito in MediaPlayerState.

Questa operazione è utile nei casi seguenti:

* Per riutilizzare un’ `MediaPlayer` istanza occorre caricarne una nuova `MediaResource` (contenuto video) e sostituire l’istanza precedente.

   La reimpostazione consente di riutilizzare l’ `MediaPlayer` istanza senza sovraccaricare le risorse, ricreare l’istanza `MediaPlayer`e riallocare le risorse.

* Quando lo stato `MediaPlayer` è ERROR e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l&#39;unico modo per recuperare dallo stato ERROR.

1. Chiamata `reset` per restituire l’ `MediaPlayer` istanza allo stato non inizializzato:

   ```java
   void reset() throws IllegalStateException; 
   ```

1. Utilizzare `MediaPlayer.replaceCurrentResource` per caricare un altro `MediaResource`.

   >[!TIP]
   >
   >Per cancellare un errore, caricate lo stesso `MediaResource`.

1. Quando ricevete il callback dell’ `STATUS_CHANGED` evento con lo stato PREPARATO, avviate la riproduzione.

## Rilasciare un’istanza e le risorse di MediaPlayer{#release-a-mediaplayer-instance-and-resources}

Rilasciare un’istanza e risorse di MediaPlayer quando non è più necessario disporre di MediaResource.

Quando si rilascia un `MediaPlayer` oggetto, le risorse hardware sottostanti associate a tale `MediaPlayer` oggetto vengono deallocate.

Di seguito sono riportati alcuni motivi per rilasciare un MediaPlayer:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Lasciare un oggetto inutile `MediaPlayer` può comportare un consumo continuo di batterie per i dispositivi mobili.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

1. Rilasciate il `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

Una volta rilasciata l&#39; `MediaPlayer` istanza, non sarà più possibile utilizzarla. Se dopo il rilascio viene chiamato un metodo dell’ `MediaPlayer` interfaccia, viene `IllegalStateException` generato un messaggio.