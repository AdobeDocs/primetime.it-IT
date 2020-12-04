---
description: Utilizzate la classe helper AuditudeSettings, che estende la classe MetadataNode, per impostare  Adobe Primetime e i metadati di decisione.
seo-description: Utilizzate la classe helper AuditudeSettings, che estende la classe MetadataNode, per impostare  Adobe Primetime e i metadati di decisione.
seo-title: Impostare e inserire i metadati
title: Impostare e inserire i metadati
uuid: 5c807fad-4927-4547-b58c-f37e505e651c
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Impostare e inserire i metadati {#set-up-ad-insertion-metadata}

Utilizzate la classe helper AuditudeSettings, che estende la classe MetadataNode, per impostare  Adobe Primetime e i metadati di decisione.

>[!TIP]
>
> il processo decisionale pubblicitario di Adobe Primetime era precedentemente noto come Auditude.

I metadati della pubblicità si trovano nella proprietà `MediaResource.Metadata`. Quando avviate la riproduzione di un nuovo video, l’applicazione è responsabile dell’impostazione dei metadati pubblicitari corretti.

1. Create l&#39;istanza `AuditudeSettings`.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Impostate i parametri di targeting  Adobe Primetime `mediaID`, `zoneID`, `<ph conkeyref="phrases/primetime-sdk-name"/>` e i parametri di targeting facoltativi.

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
   >L&#39;ID del supporto viene utilizzato da TVSDK come stringa, che viene convertita in un valore md5 e utilizzato per il valore `u` nella richiesta URL di Primetime e di decisione. Ad esempio:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Create un&#39;istanza `MediaResource` utilizzando l&#39;URL del flusso multimediale e i metadati pubblicitari creati in precedenza.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Caricate l&#39;oggetto `MediaResource` tramite il metodo `MediaPlayer.replaceCurrentResource`.

   `MediaPlayer` avvia il caricamento e l&#39;elaborazione del manifesto del flusso multimediale.

1. Quando la `MediaPlayer` passa allo stato INITIALIZED, ottenete le caratteristiche del flusso multimediale sotto forma di istanza `MediaPlayerItem` tramite il metodo `MediaPlayer.CurrentItem`.
1. (Facoltativo) Eseguite una query sull&#39;istanza `MediaPlayerItem` per verificare se il flusso è live, indipendentemente dal fatto che contenga tracce audio alternative o che il flusso sia protetto.

   Queste informazioni sono utili per preparare l’interfaccia per la riproduzione. Ad esempio, se sai che esistono due tracce audio, puoi includere un controllo dell’interfaccia utente che alterni tali tracce.

1. Chiama `MediaPlayer.prepareToPlay` per avviare il flusso di lavoro della pubblicità.

   Dopo che gli annunci sono stati risolti e inseriti nella timeline, lo stato `MediaPlayer` passa allo stato `PREPARED`.
1. Chiamate `MediaPlayer.play` per avviare la riproduzione.

TVSDK ora include annunci durante la riproduzione dei contenuti multimediali.