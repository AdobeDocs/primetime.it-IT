---
description: Utilizzate la classe helper AuditudeSettings per impostare i metadati di decisione degli annunci Adobe Primetime.
seo-description: Utilizzate la classe helper AuditudeSettings per impostare i metadati di decisione degli annunci Adobe Primetime.
seo-title: Impostare e inserire i metadati
title: Impostare e inserire i metadati
uuid: fc37e0ae-6acf-4a78-a468-f7b5b123b45e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Impostare e inserire i metadati{#set-up-ad-insertion-metadata}

Utilizzate la classe helper AuditudeSettings per impostare i metadati di decisione degli annunci Adobe Primetime.

>[!TIP]
>
>Adobe Primetime ad un processo decisionale precedentemente noto come Auditude .

1. Create l’ `AuditudeSettings` istanza.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Impostate i parametri mediaID, zoneID, dominio e di targeting facoltativi di Adobe Primetime.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Create un&#39; `MediaResource` istanza utilizzando l&#39;URL del flusso multimediale e i metadati pubblicitari creati in precedenza.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Caricate l&#39; `MediaResource` oggetto tramite il `MediaPlayer.replaceCurrentResource(resource)` metodo.

   Viene `MediaPlayer` avviato il caricamento e l&#39;elaborazione del manifesto del flusso multimediale.

1. Quando si `MediaPlayer` passa allo stato INITIALIZED, ottenere le caratteristiche del flusso multimediale nella forma di un&#39; `MediaPlayerItem` istanza tramite l&#39; `MediaPlayer.CurrentItem` attributo.
1. (Facoltativo) Eseguite una query sull&#39; `MediaPlayerItem` istanza per verificare se il flusso è live, indipendentemente dal fatto che contenga tracce audio alternative.

   Queste informazioni sono utili per preparare l’interfaccia per la riproduzione. Ad esempio, se sai che esistono due tracce audio, puoi includere un controllo dell’interfaccia utente che alterni tali tracce.

1. Chiama `MediaPlayer.prepareToPlay` per avviare il flusso di lavoro della pubblicità.

   Dopo che gli annunci sono stati risolti e inseriti nella timeline, le `  MediaPlayer ` transizioni verso lo stato PREPARATO.
1. Chiamata `MediaPlayer.play` per avviare la riproduzione.
Il browser TVSDK ora include annunci durante la riproduzione dei contenuti multimediali.
