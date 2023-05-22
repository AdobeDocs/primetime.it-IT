---
description: Per consentire il funzionamento del resolver dell’annuncio, i provider di annunci, come Adobe Primetime ad decisioning, richiedono valori di configurazione per abilitare la connessione al provider.
title: Metadati di inserimento annuncio
exl-id: 83c0fd25-dbc3-4529-b81a-16ff78012c80
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Metadati di inserimento annuncio {#ad-insertion-metadata}

Per consentire il funzionamento del resolver dell’annuncio, i provider di annunci, come Adobe Primetime ad decisioning, richiedono valori di configurazione per abilitare la connessione al provider.

TVSDK include la libreria Ad Decisioning di Primetime. Affinché il contenuto includa la pubblicità dal server Primetime ad decisioning, l’applicazione deve fornire i seguenti elementi obbligatori `AuditudeSettings` informazioni:

* `mediaID`, che è un identificatore univoco del video da riprodurre.

   L’editore assegna il mediaID quando invia il contenuto video e le informazioni sugli annunci al server Adobe Primetime ad decisioning. Questo ID viene utilizzato da Primetime ad Decisioning per recuperare dal server le informazioni pubblicitarie correlate al video.

* Il tuo `zoneID`, che viene assegnato da Adobe, identifica la tua azienda o il tuo sito web.
* Il dominio del server di annunci assegnato.
* Altri parametri di targeting.

   Puoi includere questi parametri in base alle tue esigenze e a quelle del provider di annunci.

## Impostare i metadati di inserimento annunci {#set-up-ad-insertion-metadata}

Utilizza la classe helper AuditudeSettings , che estende la classe MetadataNode, per configurare i metadati di Adobe Primetime ad decisioning.

>[!TIP]
>
>Adobe Primetime ad decisioning era precedentemente noto come Auditude.

I metadati della pubblicità si trovano in `MediaResource.metadata` proprietà. All’avvio della riproduzione di un nuovo video, l’applicazione è responsabile dell’impostazione dei metadati pubblicitari corretti.

1. Creare `AuditudeSettings` dell&#39;istanza.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings();
   ```

1. Imposta l’ID del supporto di Adobe Primetime ad decisioning, l’ID della zona, il dominio e i parametri di targeting facoltativi.

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
   >L&#39;ID del file multimediale viene utilizzato da TVSDK come stringa, che viene convertito in un valore md5 e viene utilizzato per `u` valore nella richiesta URL di Primetime ad decisioning. Ad esempio:
   >
   >
   >` https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Creare un `MediaResource` utilizzando l’URL del flusso multimediale e i metadati pubblicitari creati in precedenza.

   ```
   var mediaResourceMetadata:MetadataNode = new MetadataNode(); 
   mediaResourceMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY, auditudeSettings); 
   var mediaResource:MediaResource = new MediaResource( 
         "www.example.com/video/test.m3u8", 
         MediaResourceType.HLS,  
         mediaResourceMetadata);
   ```

1. Carica `MediaResource` oggetto tramite `MediaPlayer.replaceCurrentResource` metodo.

   Il `MediaPlayer` inizia a caricare ed elaborare il manifesto del flusso multimediale.

1. (Facoltativo) Esegui una query su `MediaPlayerItem` per vedere se il flusso è in diretta, indipendentemente dal fatto che abbia tracce audio alternative o che sia protetto.

   Queste informazioni possono essere utili per preparare l’interfaccia utente per la riproduzione. Ad esempio, se sai che esistono due tracce audio, puoi includere un controllo dell’interfaccia utente che attiva o disattiva queste tracce.

1. Chiamata `MediaPlayer.prepareToPlay` per avviare il flusso di lavoro di advertising.

   Dopo aver risolto gli annunci e averli inseriti nella timeline, il `MediaPlayer` le transizioni allo stato PREPARATO.
1. Chiamata `MediaPlayer.play` per avviare la riproduzione.

TVSDK ora include gli annunci durante la riproduzione dei contenuti multimediali.
