---
description: L'interfaccia PTMediaPlayer incapsula la funzionalità e il comportamento di un oggetto lettore multimediale.
title: Configurare PTMediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Configurare PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK fornisce gli strumenti per creare un’applicazione video player avanzata (il lettore Primetime), che puoi integrare con altri componenti di Primetime.

Utilizza gli strumenti della tua piattaforma per creare un lettore e collegarlo alla visualizzazione del lettore multimediale in TVSDK, che dispone di metodi per riprodurre e gestire i video. Ad esempio, TVSDK fornisce metodi di riproduzione e pausa. Puoi creare pulsanti dell’interfaccia utente sulla tua piattaforma e impostarli per chiamare tali metodi TVSDK.

L&#39;interfaccia PTMediaPlayer incapsula la funzionalità e il comportamento di un oggetto lettore multimediale.

Per impostare `PTMediaPlayer`:

1. Recupera l’URL del file multimediale dall’interfaccia utente, ad esempio, in un campo di testo.

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. Crea `PTMetadata`.

   Supponiamo che il tuo metodo `createMetada` prepara i metadati (vedere [Pubblicità](../ad-insertion/r-psdk-ios-1.4-advertising-requirements.md)).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. Crea `PTMediaPlayerItem` utilizzando `PTMetadata` dell&#39;istanza.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. Aggiungi osservatori alle notifiche inviate da TVSDK.

   ```
   [self addObservers]
   ```

1. Crea `PTMediaPlayer` utilizzo del nuovo `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. Imposta le proprietà sul lettore.

   Ecco alcune delle opzioni disponibili `PTMediaPlayer` proprietà:

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

1. Aggiungi la vista del lettore nella vista secondaria della vista corrente.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. Chiamata `play` per avviare la riproduzione di contenuti multimediali.

   ```
   [player play];
   ```
