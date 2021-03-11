---
description: Per consentire il funzionamento del risolutore di annunci, i fornitori di annunci, come Adobe Primetime ad decision, richiedono valori di configurazione per abilitare la connessione al provider.
title: Metadati di inserimento annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Metadati di inserimento annunci {#ad-insertion-metadata}

Per consentire il funzionamento del risolutore di annunci, i fornitori di annunci, come Adobe Primetime ad decision, richiedono valori di configurazione per abilitare la connessione al provider.

TVSDK include la libreria Primetime ad decision ioning. Affinché i contenuti includano la pubblicità dal server di ad decisioning di Primetime, l&#39;applicazione deve fornire le seguenti informazioni `AuditudeSettings` necessarie:

* `mediaID`, che è un identificatore univoco per il video da riprodurre.

   L&#39;editore assegna il mediaID quando invia contenuti video e informazioni sugli annunci al server Adobe Primetime ad decision ioning. Questo ID viene utilizzato da Primetime ad decision per recuperare dal server le informazioni pubblicitarie correlate al video.

* Il `zoneID`, assegnato per Adobe, identifica l&#39;azienda o il sito web.
* Dominio del server di annunci assegnato.
* Altri parametri di targeting.

   Puoi includere questi parametri in base alle tue esigenze e alle esigenze del provider di annunci.

## Impostare i metadati di inserimento annunci {#set-up-ad-insertion-metadata}

Utilizza la classe helper AuditudeSettings , che estende la classe MetadataNode, per configurare i metadati di Adobe Primetime e delle decisioni.

>[!TIP]
>
>Adobe Primetime ad decision era noto in precedenza come Auditude.

I metadati della pubblicità si trovano nella proprietà `MediaResource.metadata` . Quando si avvia la riproduzione di un nuovo video, l&#39;applicazione è responsabile dell&#39;impostazione dei metadati pubblicitari corretti.

1. Crea l&#39;istanza `AuditudeSettings` .

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Imposta mediaID, zoneID, dominio e i parametri di targeting facoltativi per Adobe Primetime ad decision.

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
   >L&#39;ID del file multimediale viene utilizzato da TVSDK come stringa, che viene convertita in un valore md5 e viene utilizzato per il valore `u` nella richiesta URL Primetime ad decision ioning. Ad esempio:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Crea un&#39;istanza `MediaResource` utilizzando l&#39;URL del flusso multimediale e i metadati pubblicitari creati in precedenza.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. Caricare l&#39;oggetto `MediaResource` attraverso il metodo `MediaPlayer.replaceCurrentResource`.

   Il `MediaPlayer` inizia a caricare ed elaborare il manifesto del flusso multimediale.

1. (Facoltativo) Esegui una query sull&#39;istanza `MediaPlayerItem` per verificare se il flusso è attivo, indipendentemente dal fatto che abbia tracce audio alternative o se il flusso sia protetto.

   Queste informazioni sono utili per preparare l’interfaccia utente per la riproduzione. Ad esempio, se sai che ci sono due tracce audio, puoi includere un controllo dell’interfaccia utente che passa da una traccia all’altra.

1. Chiama `MediaPlayer.prepareToPlay` per avviare il flusso di lavoro pubblicitario.

   Una volta risolti e inseriti gli annunci nella timeline, lo stato `MediaPlayer` passa allo stato PREPARATO.
1. Richiama `MediaPlayer.play` per avviare la riproduzione.

TVSDK ora include gli annunci durante la riproduzione dei contenuti multimediali.