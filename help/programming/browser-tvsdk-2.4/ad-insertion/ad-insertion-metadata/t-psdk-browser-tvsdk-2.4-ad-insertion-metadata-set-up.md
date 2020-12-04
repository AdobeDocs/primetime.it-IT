---
description: Utilizzate la classe helper AuditudeSettings per impostare  Adobe Primetime e i metadati di decisione.
seo-description: Utilizzate la classe helper AuditudeSettings per impostare  Adobe Primetime e i metadati di decisione.
seo-title: Impostare e inserire i metadati
title: Impostare e inserire i metadati
uuid: fc37e0ae-6acf-4a78-a468-f7b5b123b45e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---


# Impostazione e inserimento di metadati{#set-up-ad-insertion-metadata}

Utilizzate la classe helper AuditudeSettings per impostare  Adobe Primetime e i metadati di decisione.

>[!TIP]
>
> Adobe Primetime e le decisioni erano precedentemente noti come Auditude .

1. Create l&#39;istanza `AuditudeSettings`.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Impostate i parametri mediaID, zoneID, dominio  Adobe Primetime e di decisione dell&#39;annuncio pubblicitario e i parametri di targeting facoltativi.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Create un&#39;istanza `MediaResource` utilizzando l&#39;URL del flusso multimediale e i metadati pubblicitari creati in precedenza.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Caricate l&#39;oggetto `MediaResource` tramite il metodo `MediaPlayer.replaceCurrentResource(resource)`.

   `MediaPlayer` avvia il caricamento e l&#39;elaborazione del manifesto del flusso multimediale.

1. Quando la `MediaPlayer` passa allo stato INITIALIZED, ottenete le caratteristiche del flusso multimediale nella forma di un&#39;istanza `MediaPlayerItem` tramite l&#39;attributo `MediaPlayer.CurrentItem`.
1. (Facoltativo) Eseguite una query sull&#39;istanza `MediaPlayerItem` per verificare se il flusso è live, indipendentemente dal fatto che contenga tracce audio alternative.

   Queste informazioni sono utili per preparare l’interfaccia per la riproduzione. Ad esempio, se sai che esistono due tracce audio, puoi includere un controllo dell’interfaccia utente che alterni tali tracce.

1. Chiama `MediaPlayer.prepareToPlay` per avviare il flusso di lavoro della pubblicità.

   Dopo che gli annunci sono stati risolti e inseriti nella timeline, la transizione `  MediaPlayer ` allo stato PREPARATO.
1. Chiamate `MediaPlayer.play` per avviare la riproduzione.
Il browser TVSDK ora include annunci durante la riproduzione dei contenuti multimediali.
