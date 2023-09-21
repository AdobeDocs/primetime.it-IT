---
description: Quando si reimposta un'istanza MediaPlayer, questa viene ripristinata allo stato IDLE non inizializzato definito in MediaPlayerState.
title: Reimpostare o riutilizzare un'istanza MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Reimpostare, riutilizzare o rimuovere un&#39;istanza MediaPlayer {#reset-or-reuse-a-mediaplayer-instance}

È possibile reimpostare, riutilizzare o rilasciare un&#39;istanza di MediaPlayer non più necessaria.

Quando si reimposta un&#39;istanza MediaPlayer, questa viene ripristinata allo stato IDLE non inizializzato definito in MediaPlayerState.

Questa operazione è utile nei seguenti casi:

* Si desidera riutilizzare un `MediaPlayer` ma deve caricare un nuovo `MediaResource` (contenuto video) e sostituisci l’istanza precedente.

  Il ripristino consente di riutilizzare `MediaPlayer` senza il sovraccarico di rilasciare le risorse, ricreando il `MediaPlayer`e la riallocazione delle risorse.

* Quando `MediaPlayer` è in stato ERROR e deve essere cancellato.

  >[!IMPORTANT]
  >
  >Questo è l’unico modo per recuperare dallo stato ERROR.

1. Chiamata `reset` per restituire il `MediaPlayer` istanza al relativo stato non inizializzato:

   ```java
   void reset() throws IllegalStateException; 
   ```

1. Utilizzare `MediaPlayer.replaceCurrentResource` per caricare un altro `MediaResource`.

   >[!TIP]
   >
   >Per cancellare un errore, carica lo stesso `MediaResource`.

1. Quando ricevi il `STATUS_CHANGED` callback dell&#39;evento con stato PREPARATO, avviare la riproduzione.

## Rilasciare un’istanza MediaPlayer e le relative risorse{#release-a-mediaplayer-instance-and-resources}

È necessario rilasciare un&#39;istanza MediaPlayer e le relative risorse quando non è più necessario MediaResource.

Quando si rilascia una `MediaPlayer` oggetto, le risorse hardware sottostanti associate a questo `MediaPlayer` oggetto deallocato.

Di seguito sono riportati alcuni motivi per il rilascio di un MediaPlayer:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Lasciando un `MediaPlayer` L&#39;oggetto può causare un consumo continuo di batteria per i dispositivi mobili.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

1. Rilasciare `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

Dopo il `MediaPlayer` è stata rilasciata, non è più possibile utilizzarla. Se è stato utilizzato un metodo `MediaPlayer` viene richiamata dopo il rilascio, e `IllegalStateException` viene lanciato.
