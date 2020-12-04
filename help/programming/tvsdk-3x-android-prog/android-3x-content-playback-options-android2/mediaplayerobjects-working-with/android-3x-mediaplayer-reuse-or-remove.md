---
description: È possibile ripristinare, riutilizzare o rilasciare un'istanza di MediaPlayer non più necessaria.
seo-description: È possibile ripristinare, riutilizzare o rilasciare un'istanza di MediaPlayer non più necessaria.
seo-title: Riutilizzare o rimuovere un'istanza di MediaPlayer
title: Riutilizzare o rimuovere un'istanza di MediaPlayer
uuid: 74a46689-1708-4d26-9a4e-a4cdb0e55451
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Riutilizzare o rimuovere un&#39;istanza di MediaPlayer {#reuse-or-remove-a-mediaplayer-instance}

È possibile ripristinare, riutilizzare o rilasciare un&#39;istanza di MediaPlayer non più necessaria.

## Reimpostare o riutilizzare un&#39;istanza di MediaPlayer {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

Quando si reimposta un&#39;istanza `MediaPlayer`, viene riportato al relativo stato IDLE non inizializzato come definito in `MediaPlayerStatus`.

Questa operazione è utile nei casi seguenti:

* Per riutilizzare un&#39;istanza `MediaPlayer` è necessario caricare una nuova `MediaResource` (contenuto video) e sostituire l&#39;istanza precedente.

   La reimpostazione consente di riutilizzare l&#39;istanza `MediaPlayer` senza sovraccaricare le risorse, ricreare l&#39;istanza `MediaPlayer` e riallocare le risorse.

* Quando il `MediaPlayer` è in stato di ERRORE e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l&#39;unico modo per recuperare dallo stato di ERRORE.

   1. Chiamare `reset` per restituire l&#39;istanza `MediaPlayer` allo stato non inizializzato:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Utilizzare `MediaPlayer.replaceCurrentResource()` per caricare un altro `MediaResource`.

      >[!NOTE]
      >
      >Per cancellare un errore, caricate lo stesso `MediaResource`.

   1. Quando ricevete il callback dell&#39;evento `STATUS_CHANGED` con lo stato `PREPARED`, avviate la riproduzione.

## Rilasciare un&#39;istanza di MediaPlayer e le risorse {#section_13A0914AFF784943ABC343F7EB249C4E}

Rilasciare un&#39;istanza `MediaPlayer` e le risorse quando non è più necessario `MediaResource`.

Quando si rilascia un oggetto `MediaPlayer`, le risorse hardware sottostanti associate a questo oggetto `MediaPlayer` vengono deallocate.

Di seguito sono riportati alcuni motivi per rilasciare un `MediaPlayer`:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Lasciare un oggetto `MediaPlayer` non necessario istanziato può comportare un consumo continuo della batteria per i dispositivi mobili.
* Se più istanze
Se uno stesso codec video non è supportato su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

* Rilasciare la `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >Dopo il rilascio dell&#39;istanza `MediaPlayer`, non è più possibile utilizzarla. Se dopo il rilascio viene chiamato un metodo dell&#39;interfaccia `MediaPlayer`, viene restituito un `MediaPlayerException`.