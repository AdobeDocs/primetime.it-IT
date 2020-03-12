---
description: Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come Adobe Primetime ad Decioning, richiedono valori di configurazione per abilitare la connessione al provider.
seo-description: Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come Adobe Primetime ad Decioning, richiedono valori di configurazione per abilitare la connessione al provider.
seo-title: Aggiungi metadati di inserimento
title: Aggiungi metadati di inserimento
uuid: 3eb024c3-4bb5-4bee-943e-fe0c60379e60
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Aggiungi metadati di inserimento {#ad-insertion-metadata}

Per consentire il funzionamento del risolutore degli annunci, i fornitori di annunci, come Adobe Primetime ad Decioning, richiedono valori di configurazione per abilitare la connessione al provider.

TVSDK include la libreria Primetime e decisionali. Affinché il contenuto includa la pubblicità proveniente dal server di decisione degli annunci Primetime, l&#39;applicazione deve fornire le seguenti `AuditudeSettings` informazioni necessarie:

* `mediaID`, che è un identificatore univoco per il video da riprodurre.

   L&#39;editore assegna il mediaID quando invia contenuti video e informazioni sull&#39;annuncio al server Adobe Primetime ad Ad Decision. Questo ID viene utilizzato da Primetime ad Decioning per recuperare informazioni pubblicitarie correlate al video dal server.

* Il vostro `zoneID`, assegnato da Adobe, identifica la vostra società o il vostro sito Web.
* Il dominio del server di annunci assegnato.
* Altri parametri di targeting.

   Puoi includere questi parametri in base alle tue esigenze e alle esigenze del provider di annunci.

## Impostare e inserire i metadati {#set-up-ad-insertion-metadata}

Utilizzate la classe helper AuditudeSettings , che estende la classe MetadataNode, per configurare i metadati di decisioni pubblicitari di Adobe Primetime.

>[!TIP]
>
>Il processo di decisione degli annunci Adobe Primetime era precedentemente noto come Auditude.

I metadati della pubblicità si trovano nella `MediaResource.metadata` proprietà . Quando avviate la riproduzione di un nuovo video, l’applicazione è responsabile dell’impostazione dei metadati pubblicitari corretti.

1. Create l’ `AuditudeSettings` istanza.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Impostate i parametri mediaID, zoneID, dominio e di targeting facoltativi di Adobe Primetime.

   ```
   auditudeSettings.zoneId = "yourZoneID"; 
   auditudeSettings.mediaId = "media_identifier"; 
   auditudeSettings.domain = "yourAuditudeDomain"; 
   var targetingInfo:Metadata = new Metadata(); 
   targetingInfo.setValue("yourParamName", "yourParamValue"); 
   auditudeSettings.targetingInfo = targetingInfo;
   ```

   >[!TIP]
   >
   >L’ID file multimediale viene utilizzato da TVSDK come stringa, che viene convertita in un valore md5 e utilizzato per il `u` valore nella richiesta dell’URL Primetime e di decisione. Ad esempio:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Create un&#39; `MediaResource` istanza utilizzando l&#39;URL del flusso multimediale e i metadati pubblicitari creati in precedenza.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. Caricate l&#39; `MediaResource` oggetto tramite il `MediaPlayer.replaceCurrentResource` metodo.

   Viene `MediaPlayer` avviato il caricamento e l&#39;elaborazione del manifesto del flusso multimediale.

1. (Facoltativo) Eseguite una query sull&#39; `MediaPlayerItem` istanza per verificare se il flusso è live, indipendentemente dal fatto che contenga tracce audio alternative o che il flusso sia protetto.

   Queste informazioni sono utili per preparare l’interfaccia per la riproduzione. Ad esempio, se sai che esistono due tracce audio, puoi includere un controllo dell’interfaccia utente che alterni tali tracce.

1. Chiama `MediaPlayer.prepareToPlay` per avviare il flusso di lavoro della pubblicità.

   Dopo che gli annunci sono stati risolti e inseriti nella timeline, le `MediaPlayer` transizioni verso lo stato PREPARATO.
1. Chiamata `MediaPlayer.play` per avviare la riproduzione.

TVSDK ora include annunci durante la riproduzione dei contenuti multimediali.