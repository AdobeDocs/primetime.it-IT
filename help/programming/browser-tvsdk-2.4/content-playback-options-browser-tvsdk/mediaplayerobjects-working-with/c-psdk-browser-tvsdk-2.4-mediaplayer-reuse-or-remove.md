---
description: È possibile reimpostare, riutilizzare o rilasciare un'istanza di MediaPlayer non più necessaria.
title: Riutilizzare o rimuovere un'istanza MediaPlayer
exl-id: 2403e6dd-74c4-43fb-913a-d04e61041628
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# Riutilizzare o rimuovere un&#39;istanza MediaPlayer{#reuse-or-remove-a-mediaplayer-instance}

È possibile reimpostare, riutilizzare o rilasciare un&#39;istanza di MediaPlayer non più necessaria.

## Reimpostare o riutilizzare un&#39;istanza MediaPlayer {#section_C183E6164C184C3CBC5321FC6A2528EA}

È possibile reimpostare un `MediaPlayer` per riportarlo allo stato IDLE non inizializzato come definito in `MediaPlayerStatus`. Puoi anche sostituire l’elemento multimediale corrente o impostarne uno nuovo utilizzando una risorsa multimediale caricata in precedenza.

Questa operazione è utile nei seguenti casi:

* Si desidera riutilizzare un `MediaPlayer` ma deve caricare un nuovo `MediaResource` (contenuto video) e sostituisci l’istanza precedente.

   Il ripristino consente di riutilizzare `MediaPlayer` senza il sovraccarico di rilasciare le risorse, ricreando il `MediaPlayer`e la riallocazione delle risorse. Il `replaceCurrentItem` Il metodo esegue automaticamente questi passaggi.

* Quando `MediaPlayer` è in stato ERROR e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l’unico modo per recuperare dallo stato ERROR.

1. Chiamata `MediaPlayer.reset()` per restituire il `MediaPlayer` istanza al relativo stato non inizializzato:

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Chiamata `MediaPlayer.replaceCurrentItem()` per caricare un altro `MediaResource`

   >[!TIP]
   >
   >Per cancellare un errore, carica lo stesso `MediaResource`.

1. Chiama il `prepareToPlay()` metodo.

   >[!NOTE]
   >
   >Quando ricevi il `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` con lo stato READY, è possibile avviare la riproduzione.

## Rilasciare un’istanza MediaPlayer e le relative risorse {#section_2D159975C82245098E7078FE0B1578CE}

È necessario rilasciare una `MediaPlayer` e risorse quando non è più necessario MediaResource.

Di seguito sono riportati alcuni motivi per cui è necessario rilasciare una `MediaPlayer`:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Lasciando un `MediaPlayer` L&#39;oggetto può causare un consumo continuo di batteria per i dispositivi mobili.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

* Rilasciare `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >Dopo il `MediaPlayer` è stata rilasciata, non è più possibile utilizzarla. Se è stato utilizzato un metodo `MediaPlayer` viene richiamata dopo il rilascio, e `IllegalStateException` viene lanciato.
