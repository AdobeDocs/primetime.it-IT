---
description: Utilizza la classe helper AuditudeSettings per configurare i metadati di Adobe Primetime ad decisioning.
title: Impostare i metadati di inserimento annunci
exl-id: 03b2237b-6b3b-46cf-bc0b-691513033463
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Impostare i metadati di inserimento annunci{#set-up-ad-insertion-metadata}

Utilizza la classe helper AuditudeSettings per configurare i metadati di Adobe Primetime ad decisioning.

>[!TIP]
>
>Adobe Primetime ad decisioning era precedentemente noto come Auditude .

1. Creare `AuditudeSettings` dell&#39;istanza.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Imposta l’ID del supporto di Adobe Primetime ad decisioning, l’ID della zona, il dominio e i parametri di targeting facoltativi.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Creare un `MediaResource` utilizzando l’URL del flusso multimediale e i metadati pubblicitari creati in precedenza.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Carica `MediaResource` oggetto tramite `MediaPlayer.replaceCurrentResource(resource)` metodo.

   Il `MediaPlayer` inizia a caricare ed elaborare il manifesto del flusso multimediale.

1. Quando `MediaPlayer` allo stato INIZIALIZZATO, ottengono le caratteristiche del flusso multimediale sotto forma di `MediaPlayerItem` tramite il `MediaPlayer.CurrentItem` attributo.
1. (Facoltativo) Esegui una query su `MediaPlayerItem` per vedere se il flusso è in diretta, indipendentemente dal fatto che abbia tracce audio alternative.

   Queste informazioni possono essere utili per preparare l’interfaccia utente per la riproduzione. Ad esempio, se sai che esistono due tracce audio, puoi includere un controllo dell’interfaccia utente che attiva o disattiva queste tracce.

1. Chiamata `MediaPlayer.prepareToPlay` per avviare il flusso di lavoro di advertising.

   Dopo aver risolto gli annunci e averli inseriti nella timeline, il `  MediaPlayer ` le transizioni allo stato PREPARATO.
1. Chiamata `MediaPlayer.play` per avviare la riproduzione.
Il browser TVSDK ora include gli annunci durante la riproduzione dei contenuti multimediali.
