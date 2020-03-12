---
description: È possibile ripristinare, riutilizzare o rilasciare un'istanza di MediaPlayer non più necessaria.
seo-description: È possibile ripristinare, riutilizzare o rilasciare un'istanza di MediaPlayer non più necessaria.
seo-title: Riutilizzare o rimuovere un'istanza di MediaPlayer
title: Riutilizzare o rimuovere un'istanza di MediaPlayer
uuid: 74a46689-1708-4d26-9a4e-a4cdb0e55451
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Riutilizzare o rimuovere un&#39;istanza di MediaPlayer {#reuse-or-remove-a-mediaplayer-instance}

È possibile ripristinare, riutilizzare o rilasciare un&#39;istanza di MediaPlayer non più necessaria.

## Reimpostare o riutilizzare un&#39;istanza di MediaPlayer {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

Quando reimpostate un&#39; `MediaPlayer` istanza, questa viene restituita al relativo stato IDLE non inizializzato, come definito in `MediaPlayerStatus`.

Questa operazione è utile nei casi seguenti:

* Per riutilizzare un’ `MediaPlayer` istanza occorre caricarne una nuova `MediaResource` (contenuto video) e sostituire l’istanza precedente.

   La reimpostazione consente di riutilizzare l’ `MediaPlayer` istanza senza sovraccaricare le risorse, ricreare l’istanza `MediaPlayer`e riallocare le risorse.

* Quando lo stato `MediaPlayer` è ERROR e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l&#39;unico modo per recuperare dallo stato di ERRORE.

   1. Chiamata `reset` per ripristinare lo stato non inizializzato dell’ `MediaPlayer` istanza:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Utilizzare `MediaPlayer.replaceCurrentResource()` per caricare un altro `MediaResource`.

      >[!NOTE]
      >
      >Per cancellare un errore, caricate lo stesso `MediaResource`.

   1. Quando ricevete il callback dell’ `STATUS_CHANGED` evento con `PREPARED` lo stato, avviate la riproduzione.

## Rilasciare un’istanza e le risorse di MediaPlayer {#section_13A0914AFF784943ABC343F7EB249C4E}

Rilasciare un’ `MediaPlayer` istanza e le risorse quando non è più necessario utilizzare il `MediaResource`.

Quando si rilascia un `MediaPlayer` oggetto, le risorse hardware sottostanti associate a tale `MediaPlayer` oggetto vengono deallocate.

Di seguito sono riportati alcuni motivi per rilasciare un `MediaPlayer`:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Lasciare un oggetto non necessario `MediaPlayer` istanziato può comportare un consumo continuo della batteria per i dispositivi mobili.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

* Rilasciate il `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >Una volta rilasciata l&#39; `MediaPlayer` istanza, non sarà più possibile utilizzarla. Se dopo il rilascio viene chiamato un metodo dell’ `MediaPlayer` interfaccia, viene `MediaPlayerException` generata una chiamata.