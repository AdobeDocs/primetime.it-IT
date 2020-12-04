---
description: È possibile ripristinare, riutilizzare o rilasciare un'istanza di MediaPlayer non più necessaria.
seo-description: È possibile ripristinare, riutilizzare o rilasciare un'istanza di MediaPlayer non più necessaria.
seo-title: Riutilizzare o rimuovere un'istanza di MediaPlayer
title: Riutilizzare o rimuovere un'istanza di MediaPlayer
uuid: 0b9a06b0-ece7-4e18-9221-a4528bcbc141
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Riutilizzare o rimuovere un&#39;istanza di MediaPlayer{#reuse-or-remove-a-mediaplayer-instance}

È possibile ripristinare, riutilizzare o rilasciare un&#39;istanza di MediaPlayer non più necessaria.

## Reimpostare o riutilizzare un&#39;istanza di MediaPlayer {#section_C183E6164C184C3CBC5321FC6A2528EA}

È possibile reimpostare un&#39;istanza `MediaPlayer` per riportarla allo stato IDLE non inizializzato come definito in `MediaPlayerStatus`. È inoltre possibile sostituire l&#39;elemento multimediale corrente o impostarne uno nuovo utilizzando una risorsa multimediale precedentemente caricata.

Questa operazione è utile nei casi seguenti:

* Per riutilizzare un&#39;istanza `MediaPlayer` è necessario caricare una nuova `MediaResource` (contenuto video) e sostituire l&#39;istanza precedente.

   La reimpostazione consente di riutilizzare l&#39;istanza `MediaPlayer` senza sovraccaricare le risorse, ricreare l&#39;istanza `MediaPlayer` e riallocare le risorse. Il metodo `replaceCurrentItem` esegue automaticamente questi passaggi.

* Quando il `MediaPlayer` è in stato di errore e deve essere cancellato.

   >[!IMPORTANT]
   >
   >Questo è l&#39;unico modo per recuperare dallo stato ERROR.

1. Chiamare `MediaPlayer.reset()` per restituire l&#39;istanza `MediaPlayer` allo stato non inizializzato:

   ```js
   reset(); // returns AdobePSDK.PSDKErrorCode.SUCCESS 
            // on successful reset
   ```

1. Chiamare `MediaPlayer.replaceCurrentItem()` per caricare un altro `MediaResource`

   >[!TIP]
   >
   >Per cancellare un errore, caricate lo stesso `MediaResource`.

1. Chiamate il metodo `prepareToPlay()`.

   >[!NOTE]
   >
   >Quando ricevete l&#39;evento `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` con lo stato PREPARATO, potete avviare la riproduzione.

## Rilasciare un&#39;istanza di MediaPlayer e le risorse {#section_2D159975C82245098E7078FE0B1578CE}

Rilasciare un&#39;istanza e risorse `MediaPlayer` quando non è più necessario MediaResource.

Di seguito sono riportati alcuni motivi per rilasciare un `MediaPlayer`:

* L&#39;utilizzo di risorse non necessarie può influire sulle prestazioni.
* Lasciare un oggetto `MediaPlayer` inutile può comportare un consumo continuo di batterie per i dispositivi mobili.
* Se più istanze dello stesso codec video non sono supportate su un dispositivo, potrebbe verificarsi un errore di riproduzione per altre applicazioni.

* Rilasciare la `MediaPlayer`.

   ```js
   void release()
   ```

   >[!NOTE]
   >
   >Dopo il rilascio dell&#39;istanza `MediaPlayer`, non è più possibile utilizzarla. Se dopo il rilascio viene chiamato un metodo dell&#39;interfaccia `MediaPlayer`, viene restituito un `IllegalStateException`.

