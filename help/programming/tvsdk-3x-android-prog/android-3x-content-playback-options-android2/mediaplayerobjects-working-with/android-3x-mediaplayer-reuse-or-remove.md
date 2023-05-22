---
description: È possibile reimpostare, riutilizzare o rilasciare un'istanza di MediaPlayer non più necessaria.
title: Riutilizzare o rimuovere un'istanza MediaPlayer
exl-id: 8b84c7f1-713a-46b4-8eb7-d699a79e74b7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Riutilizzare o rimuovere un&#39;istanza MediaPlayer {#reuse-or-remove-a-mediaplayer-instance}

È possibile reimpostare, riutilizzare o rilasciare un&#39;istanza di MediaPlayer non più necessaria.

## Reimpostare o riutilizzare un&#39;istanza MediaPlayer {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

Quando si reimposta un `MediaPlayer` viene ripristinato lo stato IDLE non inizializzato come definito in `MediaPlayerStatus`.

Questa operazione è utile nei seguenti casi:

* Si desidera riutilizzare un `MediaPlayer` ma deve caricare un nuovo `MediaResource` (contenuto video) e sostituisci l’istanza precedente.

   Il ripristino consente di riutilizzare `MediaPlayer` senza il sovraccarico di rilasciare le risorse, ricreando il `MediaPlayer`e la riallocazione delle risorse.

* Quando `MediaPlayer` è nello stato ERROR e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l’unico modo per recuperare dallo stato ERROR.

   1. Chiamata `reset` per restituire il `MediaPlayer` istanza al relativo stato non inizializzato:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Utilizzare `MediaPlayer.replaceCurrentResource()` per caricare un altro `MediaResource`.

      >[!NOTE]
      >
      >Per cancellare un errore, carica lo stesso `MediaResource`.

   1. Quando ricevi il `STATUS_CHANGED` callback di evento con `PREPARED` stato, avvia la riproduzione.

## Rilasciare un’istanza MediaPlayer e le relative risorse {#section_13A0914AFF784943ABC343F7EB249C4E}

È necessario rilasciare una `MediaPlayer` e le risorse quando non hai più bisogno del `MediaResource`.

Quando si rilascia una `MediaPlayer` oggetto, le risorse hardware sottostanti associate a questo `MediaPlayer` oggetto deallocato.

Di seguito sono riportati alcuni motivi per cui è necessario rilasciare una `MediaPlayer`:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Lasciando un `MediaPlayer` l&#39;istanza dell&#39;oggetto può causare un consumo continuo di batteria per i dispositivi mobili.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

* Rilasciare `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >Dopo il `MediaPlayer` è stata rilasciata, non è più possibile utilizzarla. Se è stato utilizzato un metodo `MediaPlayer` viene chiamata dopo il rilascio, un `MediaPlayerException` viene lanciato.
