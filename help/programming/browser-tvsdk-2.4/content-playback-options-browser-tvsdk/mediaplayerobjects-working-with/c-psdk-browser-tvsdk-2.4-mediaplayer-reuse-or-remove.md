---
description: È possibile ripristinare, riutilizzare o rilasciare un'istanza di MediaPlayer non più necessaria.
seo-description: È possibile ripristinare, riutilizzare o rilasciare un'istanza di MediaPlayer non più necessaria.
seo-title: Riutilizzare o rimuovere un'istanza di MediaPlayer
title: Riutilizzare o rimuovere un'istanza di MediaPlayer
uuid: 0b9a06b0-ece7-4e18-9221-a4528bcbc141
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Riutilizzare o rimuovere un&#39;istanza di MediaPlayer{#reuse-or-remove-a-mediaplayer-instance}

È possibile ripristinare, riutilizzare o rilasciare un&#39;istanza di MediaPlayer non più necessaria.

## Reimpostare o riutilizzare un&#39;istanza di MediaPlayer {#section_C183E6164C184C3CBC5321FC6A2528EA}

Potete ripristinare un’ `MediaPlayer` istanza per riportarla allo stato IDLE non inizializzato come definito in `MediaPlayerStatus`. È inoltre possibile sostituire l&#39;elemento multimediale corrente o impostarne uno nuovo utilizzando una risorsa multimediale precedentemente caricata.

Questa operazione è utile nei casi seguenti:

* Per riutilizzare un’ `MediaPlayer` istanza occorre caricarne una nuova `MediaResource` (contenuto video) e sostituire l’istanza precedente.

   La reimpostazione consente di riutilizzare l’ `MediaPlayer` istanza senza sovraccaricare le risorse, ricreare l’istanza `MediaPlayer`e riallocare le risorse. Il `replaceCurrentItem` metodo esegue automaticamente questi passaggi.

* Quando lo stato `MediaPlayer` è ERROR e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l&#39;unico modo per recuperare dallo stato ERROR.

1. Chiamata `MediaPlayer.reset()` per restituire l’ `MediaPlayer` istanza allo stato non inizializzato:

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Chiamata `MediaPlayer.replaceCurrentItem()` per caricare un altro `MediaResource`

   >[!TIP]
   >
   >Per cancellare un errore, caricate lo stesso `MediaResource`.

1. Chiama il `prepareToPlay()` metodo.

   >[!NOTE]
   >
   >Quando ricevete l’ `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` evento con lo stato PREPARATO, potete avviare la riproduzione.

## Rilasciare un’istanza e le risorse di MediaPlayer {#section_2D159975C82245098E7078FE0B1578CE}

È necessario rilasciare un&#39; `MediaPlayer` istanza e risorse quando non è più necessario disporre di MediaResource.

Di seguito sono riportati alcuni motivi per rilasciare un `MediaPlayer`:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Lasciare un oggetto inutile `MediaPlayer` può comportare un consumo continuo di batterie per i dispositivi mobili.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

* Rilasciate il `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >Una volta rilasciata l&#39; `MediaPlayer` istanza, non sarà più possibile utilizzarla. Se dopo il rilascio viene chiamato un metodo dell’ `MediaPlayer` interfaccia, viene `IllegalStateException` generato un messaggio.

