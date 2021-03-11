---
description: L'interfaccia PTMediaPlayer incapsula la funzionalità e il comportamento di un oggetto Media Player.
title: Configurare PTMediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Configurare PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK fornisce gli strumenti per la creazione di un’applicazione di lettore video avanzata (il lettore Primetime), che puoi integrare con altri componenti Primetime.

Utilizza gli strumenti della piattaforma per creare un lettore e collegarlo alla visualizzazione del lettore multimediale in TVSDK, che dispone di metodi per riprodurre e gestire i video. Ad esempio, TVSDK fornisce metodi di riproduzione e pausa. Puoi creare pulsanti dell’interfaccia utente sulla piattaforma e impostare i pulsanti per chiamare tali metodi TVSDK.

L&#39;interfaccia PTMediaPlayer incapsula la funzionalità e il comportamento di un oggetto Media Player.

Per impostare il `PTMediaPlayer`:

1. Recupera l’URL del file multimediale dall’interfaccia utente, ad esempio in un campo di testo.

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. Crea `PTMetadata`.

   Supponi che il tuo metodo `createMetada` prepari i metadati (vedi [Pubblicità](../../ios-3x-advertising/ios-3x-advertising-requirements.md)).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. Crea `PTMediaPlayerItem` utilizzando l&#39;istanza `PTMetadata`.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. Aggiungi osservatori alle notifiche inviate da TVSDK.

   ```
   [self addObservers]
   ```

1. Crea `PTMediaPlayer` utilizzando il nuovo `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. Imposta le proprietà sul lettore.

   Di seguito sono elencate alcune delle proprietà disponibili `PTMediaPlayer` :

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. Imposta la proprietà di visualizzazione del lettore.

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. Aggiungi la visualizzazione del lettore nella visualizzazione secondaria della visualizzazione corrente.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. Chiama `play` per avviare la riproduzione multimediale.

   ```
   [player play];
   ```
