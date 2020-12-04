---
description: L'inserimento di annunci risolve gli annunci per video-on-demand (VOD), per lo streaming live e per lo streaming lineare con il tracciamento e la riproduzione di annunci. TVSDK effettua le richieste necessarie al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.
seo-description: L'inserimento di annunci risolve gli annunci per video-on-demand (VOD), per lo streaming live e per lo streaming lineare con il tracciamento e la riproduzione di annunci. TVSDK effettua le richieste necessarie al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.
seo-title: Inserire annunci
title: Inserire annunci
uuid: 6fffb340-65ea-4c47-a55b-c0ec4917d37c
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---


# Inserisci annunci{#insert-ads}

L&#39;inserimento di annunci risolve gli annunci per video-on-demand (VOD), per lo streaming live e per lo streaming lineare con il tracciamento e la riproduzione di annunci. TVSDK effettua le richieste necessarie al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.

Un *`ad break`* contiene uno o più annunci che vengono riprodotti in sequenza. TVSDK inserisce gli annunci nel contenuto principale come membri di una o più interruzioni pubblicitarie.

>[!TIP]
>
>Se l’annuncio contiene errori, TVSDK ignora l’annuncio.

## Risolvere e inserire annunci VOD {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK supporta diversi casi d’uso per la risoluzione e l’inserimento di annunci VOD.

* Inserimento di annunci pre-roll, dove gli annunci vengono inseriti all&#39;inizio del contenuto.
* Inserimento di annunci mid-roll, dove viene inserito almeno un annuncio al centro del contenuto.
* Inserimento di annunci postroll, in cui alla fine del contenuto viene aggiunto almeno un annuncio.

TVSDK risolve gli annunci, inserisce gli annunci nelle posizioni definite dal server di annunci e calcola la timeline virtuale prima dell&#39;avvio della riproduzione. Dopo l&#39;avvio della riproduzione, non è possibile apportare modifiche, ad esempio inserire annunci o rimuovere annunci.

## Risoluzione e inserimento di annunci live e lineari {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK supporta diversi casi di utilizzo per la risoluzione e l&#39;inserimento di annunci live e lineari.

* Inserimento di annunci pre-roll, dove viene inserito almeno un annuncio all&#39;inizio del contenuto.
* Inserimento di annunci mid-roll, dove viene inserito almeno un annuncio al centro del contenuto.

TVSDK risolve gli annunci e inserisce gli annunci quando viene rilevato un cue point nel flusso live o lineare. Per impostazione predefinita, TVSDK supporta i segnali seguenti come indicatori di annunci validi per la risoluzione e il posizionamento degli annunci:

* # EXT-X-CUEPOINT
* # EXT-X-AD
* # EXT-X-CUE
* # EXT-X-CUE-OUT

Questi marcatori richiedono l&#39;indicazione `DURATION` in secondi del campo di metadati e l&#39;ID univoco del cue point. Ad esempio:

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

Per ulteriori informazioni sui suggerimenti aggiuntivi, vedere [Iscriviti ai tag personalizzati](../ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-custom-tags-subscribe.md).

## Track client ad {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK monitora automaticamente gli annunci per VOD e lo streaming live/lineare.

Le notifiche vengono utilizzate per informare l&#39;applicazione sull&#39;avanzamento di un annuncio pubblicitario, incluse informazioni su quando inizia e quando termina.

## Implementazione di un ritorno anticipato all&#39;interruzione dell&#39;annuncio {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

Per l&#39;inserimento di annunci in streaming dal vivo, potrebbe essere necessario uscire da un&#39;interruzione di annuncio prima che tutti gli annunci nell&#39;interruzione siano riprodotti al completamento.

Di seguito sono riportati alcuni esempi di restituzione anticipata delle interruzioni pubblicitarie:

* La durata della pausa pubblicitaria in alcuni eventi sportivi.

   Sebbene sia stata specificata una durata predefinita, se il gioco riprende prima del termine dell&#39;interruzione, l&#39;interruzione dell&#39;annuncio deve essere terminata.
* Un segnale di emergenza durante un&#39;interruzione pubblicitaria in un flusso live.

La possibilità di uscire dall&#39;inizio di un&#39;interruzione dell&#39;annuncio è identificata tramite un tag personalizzato nel manifesto noto come plug-in o tag di cue-in. TVSDK consente all’applicazione di sottoscrivere questi tag di collegamento per fornire un’opportunità di accesso facilitato.

* Per utilizzare il tag `#EXT-X-CUE-IN` come opportunità di inclusione e implementare un ritorno a capo rapido all&#39;interruzione dell&#39;annuncio:

   1. Iscriviti al tag .

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. Aggiungete il risolutore di opportunità di cue-in.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* Per condividere lo stesso tag per le giunzioni a capo e a capo:

   1. Se l&#39;applicazione condivide lo stesso cue point per indicare cue out/splice-out e cue-in/splice-in, estendere `PTDefaultAdOpportunityResolver` e implementare il metodo `preparePlacementOpportunity`.

      >[!TIP]
      >
      >Il codice seguente presuppone che l&#39;app disponga di un&#39;implementazione per il metodo `isCueInOpportunity`.
      >
      >
      ```
      >- (PTPlacementOpportunity *)preparePlacementOpportunity:(PTTimedMetadata *)timedMetadata 
      >{ 
      >       if ([self isCueInOpportunity:timedMetadata]) 
      >       { 
      >               return [PTPlacementOpportunity advertisementSpliceInOpportunityWithTimedMetadata:timedMetadata]; 
      >       } 
      >       else 
      >       { 
      >               return [super preparePlacementOpportunity:timedMetadata]; 
      >       } 
      >}
      >```

   1. Registra il risolutore di opportunità esteso nell&#39;istanza `PTDefaultMediaPlayerClientFactory`.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Clear existing resolver and register the new opportunity resolver 
      [clientFactory clearOpportunityResolvers]; 
      [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
      ```

