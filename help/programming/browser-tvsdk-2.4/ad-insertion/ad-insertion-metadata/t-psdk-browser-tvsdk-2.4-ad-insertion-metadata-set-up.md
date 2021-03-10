---
description: Utilizza la classe helper AuditudeSettings per configurare i metadati di Adobe Primetime ad decision ioning.
title: Impostare i metadati di inserimento annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---


# Impostare i metadati di inserimento annunci{#set-up-ad-insertion-metadata}

Utilizza la classe helper AuditudeSettings per configurare i metadati di Adobe Primetime ad decision ioning.

>[!TIP]
>
>Adobe Primetime ad Decioning era noto in precedenza come Auditude .

1. Crea l&#39;istanza `AuditudeSettings` .

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Imposta mediaID, zoneID, dominio e i parametri di targeting facoltativi per Adobe Primetime ad decision.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Crea un&#39;istanza `MediaResource` utilizzando l&#39;URL del flusso multimediale e i metadati pubblicitari creati in precedenza.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Caricare l&#39;oggetto `MediaResource` attraverso il metodo `MediaPlayer.replaceCurrentResource(resource)`.

   Il `MediaPlayer` inizia a caricare ed elaborare il manifesto del flusso multimediale.

1. Quando il `MediaPlayer` passa allo stato INITIALIZED, ottieni le caratteristiche del flusso multimediale sotto forma di un&#39;istanza `MediaPlayerItem` tramite l&#39;attributo `MediaPlayer.CurrentItem` .
1. (Facoltativo) Esegui una query sull&#39;istanza `MediaPlayerItem` per verificare se il flusso è attivo, indipendentemente dal fatto che disponga di tracce audio alternative.

   Queste informazioni sono utili per preparare l’interfaccia utente per la riproduzione. Ad esempio, se sai che ci sono due tracce audio, puoi includere un controllo dell’interfaccia utente che passa da una traccia all’altra.

1. Chiama `MediaPlayer.prepareToPlay` per avviare il flusso di lavoro pubblicitario.

   Una volta risolti e inseriti gli annunci nella timeline, lo stato `  MediaPlayer ` passa allo stato PREPARATO.
1. Richiama `MediaPlayer.play` per avviare la riproduzione.
Il browser TVSDK ora include gli annunci durante la riproduzione dei contenuti multimediali.
