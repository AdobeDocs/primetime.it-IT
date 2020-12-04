---
description: L'interfaccia PTMediaPlayer racchiude le funzionalità e il comportamento di un oggetto Media Player.
seo-description: L'interfaccia PTMediaPlayer racchiude le funzionalità e il comportamento di un oggetto Media Player.
seo-title: Configurare PTMediaPlayer
title: Configurare PTMediaPlayer
uuid: 698034d3-1260-416f-83b0-6b7d058750a0
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Configurare PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK fornisce strumenti per la creazione di un’applicazione per lettori video avanzata (il lettore Primetime), che potete integrare con altri componenti Primetime.

Utilizzate gli strumenti della piattaforma per creare un lettore e collegarlo alla visualizzazione del lettore multimediale in TVSDK, che dispone di metodi per riprodurre e gestire i video. Ad esempio, TVSDK fornisce metodi di riproduzione e pausa. Potete creare pulsanti dell’interfaccia utente sulla piattaforma e impostare i pulsanti per chiamare tali metodi TVSDK.

L&#39;interfaccia PTMediaPlayer racchiude le funzionalità e il comportamento di un oggetto Media Player.

Per impostare il `PTMediaPlayer`:

1. Recuperate l&#39;URL del file multimediale dall&#39;interfaccia utente, ad esempio in un campo di testo.

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. Creare `PTMetadata`.

   Si supponga che il metodo `createMetada` prepari i metadati (vedere [Annuncio](../../ios-3x-advertising/ios-3x-advertising-requirements.md)).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. Creare `PTMediaPlayerItem` utilizzando l&#39;istanza `PTMetadata`.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. Aggiungete osservatori alle notifiche inviate da TVSDK.

   ```
   [self addObservers]
   ```

1. Crea `PTMediaPlayer` utilizzando la nuova `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. Impostare le proprietà sul lettore.

   Di seguito sono elencate alcune delle proprietà `PTMediaPlayer` disponibili:

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. Impostare la proprietà view del lettore.

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. Aggiungete la vista del lettore nella vista secondaria della vista corrente.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. Chiamate `play` per avviare la riproduzione multimediale.

   ```
   [player play];
   ```
