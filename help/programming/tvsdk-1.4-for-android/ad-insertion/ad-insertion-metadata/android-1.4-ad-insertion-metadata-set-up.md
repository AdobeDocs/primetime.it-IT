---
description: Utilizzate la classe helper AuditudeSettings, che estende la classe MetadataNode, per configurare i metadati di decisioni e annunci di Adobe Primetime.
seo-description: Utilizzate la classe helper AuditudeSettings, che estende la classe MetadataNode, per configurare i metadati di decisioni e annunci di Adobe Primetime.
seo-title: Impostare e inserire i metadati
title: Impostare e inserire i metadati
uuid: d96e67c3-4cc7-4309-a2a2-ff5193b46534
translation-type: tm+mt
source-git-commit: 4102780d0c7d0b96d120c1c2b3d14c47bc1b0e6f

---


# Impostare e inserire i metadati {#set-up-ad-insertion-metadata}

Utilizzate la classe helper AuditudeSettings, che estende la classe MetadataNode, per configurare i metadati di decisioni e annunci di Adobe Primetime.

>[!TIP]
>
>Il processo di decisione degli annunci Adobe Primetime era precedentemente noto come Auditude.

I metadati della pubblicità si trovano nella `MediaResource.Metadata` proprietà . Quando avviate la riproduzione di un nuovo video, l’applicazione è responsabile dell’impostazione dei metadati pubblicitari corretti.

1. Create l’ `AuditudeSettings` istanza.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Impostate i parametri di definizione degli annunci Adobe Primetime `mediaID`, `zoneID`e `domain`i parametri di targeting facoltativi.

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
   >L’ID file multimediale viene utilizzato da TVSDK come stringa, che viene convertita in un valore md5 e utilizzato per il `u` valore nella richiesta dell’URL Primetime e di decisione. Ad esempio:
   >
   >
   ```
   >https://ad.auditude.com/adserver?
   >u=c76d04ee31c91c4ce5c8cee41006c97d
   >   &z=114100 
   >   &l=20150206141527 
   >   &of=1.4 
   >   &tm=15 
   >   &g=1000002
   >```

1. Create un&#39; `MediaResource` istanza utilizzando l&#39;URL del flusso multimediale e i metadati pubblicitari creati in precedenza.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Caricate l&#39; `MediaResource` oggetto tramite il `MediaPlayer.replaceCurrentResource` metodo.

   Viene `MediaPlayer` avviato il caricamento e l&#39;elaborazione del manifesto del flusso multimediale.

1. Quando `MediaPlayer` si passa allo `INITIALIZED` stato, ottenete le caratteristiche del flusso multimediale nella forma di un&#39; `MediaPlayerItem` istanza tramite il `MediaPlayer.CurrentItem` metodo.
1. (Facoltativo) Eseguite una query sull&#39; `MediaPlayerItem` istanza per verificare se il flusso è live, indipendentemente dal fatto che contenga tracce audio alternative o che il flusso sia protetto.

   Queste informazioni sono utili per preparare l’interfaccia per la riproduzione. Ad esempio, se sai che esistono due tracce audio, puoi includere un controllo dell’interfaccia utente che alterni tali tracce.

1. Chiama `MediaPlayer.prepareToPlay` per avviare il flusso di lavoro della pubblicità.

   Dopo che gli annunci sono stati risolti e inseriti nella timeline, le `MediaPlayer` transizioni verso lo `PREPARED` stato.
1. Chiamata `MediaPlayer.play` per avviare la riproduzione.

TVSDK ora include annunci durante la riproduzione dei contenuti multimediali.
