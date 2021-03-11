---
description: L’inserimento di annunci risolve gli annunci per video-on-demand (VOD) , per streaming live e per streaming lineare con tracciamento degli annunci e riproduzione di annunci. TVSDK invia le richieste richieste al server di annunci, riceve le informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.
title: Inserisci annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Inserisci annunci{#insert-ads}

L’inserimento di annunci risolve gli annunci per video-on-demand (VOD) , per streaming live e per streaming lineare con tracciamento degli annunci e riproduzione di annunci. TVSDK invia le richieste richieste al server di annunci, riceve le informazioni sugli annunci per il contenuto specificato e inserisce gli annunci nel contenuto in più fasi.

Un *`ad break`* contiene uno o più annunci che vengono riprodotti in sequenza. TVSDK inserisce gli annunci nel contenuto principale come membri di una o più interruzioni pubblicitarie.

>[!TIP]
>
>Se l’annuncio contiene errori, TVSDK ignora l’annuncio.

## Risolvere e inserire annunci VOD {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK supporta diversi casi d’uso per la risoluzione e l’inserimento di annunci VOD.

* Inserimento di annunci pre-roll, in cui gli annunci vengono inseriti all’inizio del contenuto.
* Inserimento di annunci a scorrimento medio, in cui almeno un annuncio viene inserito al centro del contenuto.
* Inserimento di annunci post-roll, in cui alla fine del contenuto viene aggiunto almeno un annuncio.

TVSDK risolve gli annunci, inserisce gli annunci nelle posizioni definite dal server di annunci e calcola la timeline virtuale prima dell&#39;avvio della riproduzione. Dopo l’avvio della riproduzione, non possono verificarsi modifiche, ad esempio annunci inseriti o annunci inseriti rimossi.

## Risolvi e inserisci annunci live e lineari {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK supporta diversi casi d’uso per la risoluzione e l’inserimento di annunci in tempo reale e lineare.

* Inserimento di annunci pre-roll, in cui viene inserito almeno un annuncio all’inizio del contenuto.
* Inserimento di annunci a scorrimento medio, in cui almeno un annuncio viene inserito al centro del contenuto.

TVSDK risolve gli annunci e inserisce gli annunci quando viene rilevato un punto di cue nel flusso live o lineare. Per impostazione predefinita, TVSDK supporta i segnali seguenti come indicatori di annunci validi per la risoluzione e il posizionamento degli annunci:

* # EXT-X-CUEPOINT
* # EXT-X-AD
* # EXT-X-CUE
* # EXT-X-CUE-OUT

Questi marcatori richiedono il valore `DURATION` del campo metadati in secondi e l’ID univoco del cue. Ad esempio:

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

Per ulteriori informazioni sugli indizi aggiuntivi, consulta [Iscriviti ai tag personalizzati](../ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-custom-tags-subscribe.md).

## Tracciare gli annunci client {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK traccia automaticamente gli annunci per VOD e lo streaming live/lineare.

Le notifiche vengono utilizzate per informare l&#39;applicazione sull&#39;avanzamento di un annuncio, incluse informazioni su quando inizia e quando termina.

## Implementa un ritorno anticipato dell&#39;interruzione pubblicitaria {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

Per l&#39;inserimento di annunci in streaming live, potrebbe essere necessario uscire da un&#39;interruzione pubblicitaria prima che tutti gli annunci nell&#39;interruzione siano riprodotti al completamento.

Di seguito sono riportati alcuni esempi di ritorno anticipato dell’interruzione pubblicitaria:

* La durata della pausa pubblicitaria in alcuni eventi sportivi.

   Anche se viene fornita una durata predefinita, se il gioco riprende prima del termine dell&#39;interruzione, l&#39;interruzione pubblicitaria deve essere chiusa.
* Un segnale di emergenza durante una pausa pubblicitaria in un flusso live.

La possibilità di uscire in anticipo da un’interruzione pubblicitaria è identificata tramite un tag personalizzato nel manifesto noto come cercapersone o tag cue-in. TVSDK consente all’applicazione di abbonarsi a questi tag di collegamento diretto per fornire un’opportunità di accesso facilitato.

* Per utilizzare il tag `#EXT-X-CUE-IN` come opportunità di accesso rapido e implementare un ritorno a capo dell’annuncio:

   1. Iscriviti al tag .

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. Aggiungi il risolutore di opportunità di cue-in.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* Per condividere lo stesso tag per splice-out e splice-in:

   1. Se l&#39;applicazione condivide lo stesso cue per indicare cue-out/splice-out e cue-in/splice-in, estendere `PTDefaultAdOpportunityResolver` e implementare il metodo `preparePlacementOpportunity`.

      >[!TIP]
      >
      >Il codice seguente presuppone che l&#39;app abbia un&#39;implementazione per il metodo `isCueInOpportunity` .
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

   1. Registra il risolutore di opportunità esteso sull&#39;istanza `PTDefaultMediaPlayerClientFactory`.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Clear existing resolver and register the new opportunity resolver 
      [clientFactory clearOpportunityResolvers]; 
      [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
      ```

