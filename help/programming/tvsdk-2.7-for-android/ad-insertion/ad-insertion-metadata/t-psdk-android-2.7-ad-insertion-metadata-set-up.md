---
description: Utilizza la classe helper AuditudeSettings, che estende la classe MetadataNode, per impostare i metadati di Adobe Primetime ad decisioning.
title: Impostare i metadati di inserimento annunci
exl-id: da5bfdc1-2c55-45f2-b2a8-3e32450cb30d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# Impostare i metadati di inserimento annunci {#set-up-ad-insertion-metadata}

Utilizza la classe helper AuditudeSettings, che estende la classe MetadataNode, per impostare i metadati di Adobe Primetime ad decisioning.

>[!TIP]
>
>Adobe Primetime ad decisioning era precedentemente noto come Auditude.

I metadati della pubblicità si trovano in `MediaResource.Metadata` proprietà. All’avvio della riproduzione di un nuovo video, l’applicazione è responsabile dell’impostazione dei metadati pubblicitari corretti.

1. Creare `AuditudeSettings` dell&#39;istanza.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Impostare Adobe Primetime ad decisioning `mediaID`, `zoneID`, `<ph conkeyref="phrases/primetime-sdk-name"/>`e i parametri di targeting facoltativi.

   ```java
   auditudeSettings.setZoneId("yourZoneId"); 
   auditudeSettings.setMediaId("yourVideoId"); 
   auditudeSettings.setDefaultMediaId("defVideoId"); 
   auditudeSettings.setDomain("yourAuditudeDomain"); 
   
   // Optionally set user agent  
   auditudeSettings.setUserAgent("yourUserAgent"); 
   
   Metadata targetingParameters = new Metadata(); 
   targetingParameters.setValue("desired_param", "desired_value"); 
   auditudeSettings.setTargetingParameters(targetingParameters);
   ```

   >[!TIP]
   >
   >L&#39;ID del file multimediale viene utilizzato da TVSDK come stringa, che viene convertito in un valore md5 e viene utilizzato per `u` valore nella richiesta URL di Primetime ad decisioning. Ad esempio:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Creare un `MediaResource` utilizzando l’URL del flusso multimediale e i metadati pubblicitari creati in precedenza.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Carica `MediaResource` oggetto tramite `MediaPlayer.replaceCurrentResource` metodo.

   Il `MediaPlayer` inizia a caricare ed elaborare il manifesto del flusso multimediale.

1. Quando `MediaPlayer` allo stato INIZIALIZZATO, ottengono le caratteristiche del flusso multimediale sotto forma di `MediaPlayerItem` tramite il `MediaPlayer.CurrentItem` metodo.
1. (Facoltativo) Esegui una query su `MediaPlayerItem` per vedere se il flusso è in diretta, indipendentemente dal fatto che abbia tracce audio alternative o che il flusso sia protetto.

   Queste informazioni possono essere utili per preparare l’interfaccia utente per la riproduzione. Ad esempio, se sai che esistono due tracce audio, puoi includere un controllo dell’interfaccia utente che attiva o disattiva queste tracce.

1. Chiamata `MediaPlayer.prepareToPlay` per avviare il flusso di lavoro di advertising.

   Dopo aver risolto gli annunci e averli inseriti nella timeline, il `MediaPlayer` transizioni a `PREPARED` stato.
1. Chiamata `MediaPlayer.play` per avviare la riproduzione.

TVSDK ora include gli annunci durante la riproduzione dei contenuti multimediali.
