---
description: L’inserimento di annunci risolve gli annunci per video on-demand (VOD) , per lo streaming live e per lo streaming lineare con tracciamento degli annunci e riproduzione degli annunci. TVSDK effettua le richieste richieste richieste al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in fasi.
title: Inserisci annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Inserisci annunci {#insert-ads}

L’inserimento di annunci risolve gli annunci per video on-demand (VOD) , per lo streaming live e per lo streaming lineare con tracciamento degli annunci e riproduzione degli annunci. TVSDK effettua le richieste richieste richieste al server di annunci, riceve informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in fasi.

Un *`ad break`* contiene uno o più annunci riprodotti in sequenza. TVSDK inserisce gli annunci nel contenuto principale come membri di una o più interruzioni pubblicitarie.

>[!TIP]
>
>Se l’annuncio presenta errori, TVSDK lo ignora.

## Risolvere e inserire annunci VOD {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK supporta diversi casi d’uso per la risoluzione e l’inserimento di annunci VOD.

* Inserimento di annunci pre-roll, in cui gli annunci vengono inseriti all’inizio del contenuto.
* Inserimento di annunci mid-roll, in cui almeno un annuncio viene inserito al centro del contenuto.
* Inserimento di annunci post-roll, in cui almeno un annuncio viene aggiunto alla fine del contenuto.

TVSDK risolve gli annunci, li inserisce nelle posizioni definite dal server di annunci e calcola la timeline virtuale prima dell’inizio della riproduzione. Dopo l’avvio della riproduzione, non si possono verificare modifiche, come l’inserimento o la rimozione di annunci inseriti.

## Risoluzione e inserimento di annunci live e lineari {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK supporta diversi casi d’uso per la risoluzione e l’inserimento di annunci live e lineari.

* Inserimento di annunci pre-roll, in cui almeno un annuncio viene inserito all’inizio del contenuto.
* Inserimento di annunci mid-roll, in cui almeno un annuncio viene inserito al centro del contenuto.

TVSDK risolve gli annunci e inserisce gli annunci quando si incontra un punto di cue nel flusso live o lineare. Per impostazione predefinita, TVSDK supporta i seguenti suggerimenti come marcatori di annunci validi durante la risoluzione e il posizionamento degli annunci:

* #EXT-X-CUEPOINT
* #EXT-X-AD
* #EXT-X-CUE
* #EXT-X-CUE-OUT

Questi marcatori richiedono i `DURATION` in secondi e l’ID univoco del cue. Ad esempio:

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

Per ulteriori informazioni sui segnali aggiuntivi, consulta [Iscriviti a tag personalizzati](../../tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-custom-tags-configure/ios-3x-custom-tags-subscribe.md).

## Tracciare l’annuncio client {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK tiene traccia automaticamente degli annunci per VOD e streaming live/lineare.

Le notifiche vengono utilizzate per informare l’applicazione sull’avanzamento di un annuncio, incluse informazioni su quando inizia e termina un annuncio.

## Implementare un ritorno rapido dell’annuncio pubblicitario {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

Per l’inserimento di annunci in streaming live, potrebbe essere necessario uscire da un’interruzione pubblicitaria prima che tutti gli annunci dell’interruzione vengano riprodotti fino al completamento.

Di seguito sono riportati alcuni esempi di ritorno rapido dell’annuncio:

* La durata dell’interruzione pubblicitaria in alcuni eventi sportivi.

  Anche se viene fornita una durata predefinita, se il gioco riprende prima del termine dell’interruzione, l’interruzione pubblicitaria deve essere chiusa.
* Un segnale di emergenza durante un’interruzione pubblicitaria in un flusso live.

La possibilità di uscire anticipatamente da un’interruzione pubblicitaria viene identificata tramite un tag personalizzato nel manifesto noto come tag di collegamento o tag di collegamento. TVSDK consente all&#39;applicazione di sottoscrivere questi tag di unione per fornire un&#39;opportunità di unione.

* Per utilizzare `#EXT-X-CUE-IN` tag come opportunità di collegamento e implementazione di un ritorno rapido dell’annuncio:

   1. Iscriviti al tag.

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. Aggiungi il risolutore opportunità di cue-in.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* Per condividere lo stesso tag per giunzione e giunzione:

1. Se l&#39;applicazione condivide lo stesso segnale per indicare il cue-out/splice-out e il cue-in/splice-in, estendere `PTDefaultAdOpportunityResolver` e implementare `preparePlacementOpportunity` metodo.

   >[!TIP]
   >
   >Il codice seguente presuppone che l&#39;app abbia un&#39;implementazione per `isCueInOpportunity` metodo.

   ```
   - (PTPlacementOpportunity *)preparePlacementOpportunity:(PTTimedMetadata *)timedMetadata 
   { 
         if ([self isCueInOpportunity:timedMetadata]) 
         { 
               return [PTPlacementOpportunity advertisementSpliceInOpportunityWithTimedMetadata:timedMetadata]; 
           } 
           else 
           { 
               return [super preparePlacementOpportunity:timedMetadata]; 
         } 
   }
   ```

1. Registra il sistema di risoluzione delle opportunità estese in `PTDefaultMediaPlayerClientFactory` dell&#39;istanza.

```
   // self.player is the PTMediaPlayer instance created for content and ad playback 
       PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
             
   // Clear existing resolver and register the new opportunity resolver 
   [clientFactory clearOpportunityResolvers]; 
   [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
```
