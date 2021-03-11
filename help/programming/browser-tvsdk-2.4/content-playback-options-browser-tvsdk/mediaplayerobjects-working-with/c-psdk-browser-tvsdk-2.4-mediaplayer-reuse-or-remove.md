---
description: È possibile reimpostare, riutilizzare o rilasciare un'istanza MediaPlayer non più necessaria.
title: Riutilizzare o rimuovere un'istanza MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---


# Riutilizzare o rimuovere un&#39;istanza MediaPlayer{#reuse-or-remove-a-mediaplayer-instance}

È possibile reimpostare, riutilizzare o rilasciare un&#39;istanza MediaPlayer non più necessaria.

## Reimpostare o riutilizzare un&#39;istanza di MediaPlayer {#section_C183E6164C184C3CBC5321FC6A2528EA}

È possibile reimpostare un&#39;istanza `MediaPlayer` per riportarla al relativo stato IDLE non inizializzato come definito in `MediaPlayerStatus`. È inoltre possibile sostituire l&#39;elemento multimediale corrente o impostarne uno nuovo utilizzando una risorsa multimediale caricata in precedenza.

Questa operazione è utile nei casi seguenti:

* Desideri riutilizzare un&#39;istanza `MediaPlayer` ma devi caricare una nuova `MediaResource` (contenuto video) e sostituire l&#39;istanza precedente.

   La reimpostazione consente di riutilizzare l’istanza `MediaPlayer` senza sovraccaricare le risorse rilasciate, ricreare l’ `MediaPlayer` e riallocare le risorse. Il metodo `replaceCurrentItem` esegue automaticamente questi passaggi al posto tuo.

* Quando il `MediaPlayer` si trova in uno stato ERROR e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l&#39;unico modo per recuperare dallo stato ERROR.

1. Invoca `MediaPlayer.reset()` per restituire l&#39;istanza `MediaPlayer` al suo stato non inizializzato:

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Invoca `MediaPlayer.replaceCurrentItem()` per caricare un altro `MediaResource`

   >[!TIP]
   >
   >Per cancellare un errore, carica lo stesso `MediaResource`.

1. Chiama il metodo `prepareToPlay()` .

   >[!NOTE]
   >
   >Quando si riceve l&#39;evento `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` con lo stato PREPARATO, è possibile avviare la riproduzione.

## Rilascia un&#39;istanza e risorse MediaPlayer {#section_2D159975C82245098E7078FE0B1578CE}

Rilasciare un&#39;istanza e risorse `MediaPlayer` quando non è più necessario MediaResource.

Di seguito sono riportati alcuni motivi per rilasciare un `MediaPlayer`:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Lasciare un oggetto `MediaPlayer` non necessario può comportare un consumo continuo di batterie per i dispositivi mobili.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

* Rilascia il `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >Una volta rilasciata l’istanza `MediaPlayer`, non puoi più utilizzarla. Se dopo il rilascio viene chiamato un metodo dell&#39;interfaccia `MediaPlayer` , viene lanciato un `IllegalStateException` .

