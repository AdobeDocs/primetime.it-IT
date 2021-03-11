---
description: Utilizza la classe helper AuditudeSettings, che estende la classe MetadataNode, per configurare i metadati di Adobe Primetime e delle decisioni.
title: Impostare i metadati di inserimento annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# Impostare i metadati di inserimento annunci {#set-up-ad-insertion-metadata}

Utilizza la classe helper AuditudeSettings, che estende la classe MetadataNode, per configurare i metadati di Adobe Primetime e delle decisioni.

>[!TIP]
>
>Adobe Primetime ad decision era noto in precedenza come Auditude.

I metadati della pubblicità si trovano nella proprietà `MediaResource.Metadata` . Quando si avvia la riproduzione di un nuovo video, l&#39;applicazione è responsabile dell&#39;impostazione dei metadati pubblicitari corretti.

1. Crea l&#39;istanza `AuditudeSettings` .

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Imposta i parametri di targeting facoltativi `mediaID`, `zoneID`, `<ph conkeyref="phrases/primetime-sdk-name"/>` di Adobe Primetime e .

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
   >L&#39;ID del file multimediale viene utilizzato da TVSDK come stringa, che viene convertita in un valore md5 e viene utilizzato per il valore `u` nella richiesta URL Primetime ad decision ioning. Ad esempio:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Crea un&#39;istanza `MediaResource` utilizzando l&#39;URL del flusso multimediale e i metadati pubblicitari creati in precedenza.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Caricare l&#39;oggetto `MediaResource` attraverso il metodo `MediaPlayer.replaceCurrentResource`.

   Il `MediaPlayer` inizia a caricare ed elaborare il manifesto del flusso multimediale.

1. Quando il `MediaPlayer` passa allo stato INITIALIZED, ottieni le caratteristiche del flusso multimediale sotto forma di un&#39;istanza `MediaPlayerItem` tramite il metodo `MediaPlayer.CurrentItem` .
1. (Facoltativo) Esegui una query sull&#39;istanza `MediaPlayerItem` per verificare se il flusso è attivo, indipendentemente dal fatto che disponga di tracce audio alternative o che il flusso sia protetto.

   Queste informazioni sono utili per preparare l’interfaccia utente per la riproduzione. Ad esempio, se sai che ci sono due tracce audio, puoi includere un controllo dell’interfaccia utente che passa da una traccia all’altra.

1. Chiama `MediaPlayer.prepareToPlay` per avviare il flusso di lavoro pubblicitario.

   Una volta risolti e inseriti gli annunci nella timeline, lo stato `MediaPlayer` passa allo stato `PREPARED` .
1. Richiama `MediaPlayer.play` per avviare la riproduzione.

TVSDK ora include gli annunci durante la riproduzione dei contenuti multimediali.