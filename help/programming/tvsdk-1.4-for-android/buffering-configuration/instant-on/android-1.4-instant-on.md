---
description: Il termine "instant on" si riferisce al precaricamento di uno o più canali in modo che l'utente che seleziona un canale o che cambia canale visualizzi immediatamente il contenuto. Il buffering è già eseguito al momento in cui l'utente inizia a guardare.
seo-description: Il termine "instant on" si riferisce al precaricamento di uno o più canali in modo che l'utente che seleziona un canale o che cambia canale visualizzi immediatamente il contenuto. Il buffering è già eseguito al momento in cui l'utente inizia a guardare.
seo-title: Instant on
title: Instant on
uuid: 4cb4d221-170f-46e8-af26-32f259377617
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Instant on {#instant-on}

Il termine &quot;instant on&quot; si riferisce al precaricamento di uno o più canali in modo che l&#39;utente che seleziona un canale o che cambia canale visualizzi immediatamente il contenuto. Il buffering è già eseguito al momento in cui l&#39;utente inizia a guardare.

Senza l’attivazione immediata, TVSDK inizializza il file multimediale da riprodurre ma non avvia il buffering del flusso fino a quando l’applicazione effettua le chiamate `play`. L&#39;utente non vede alcun contenuto fino al completamento del buffering. Con l’opzione Attivato immediato, potete avviare più istanze di lettore multimediale (o caricatore di elementi per il lettore multimediale) e TVSDK avvia immediatamente la memorizzazione dei flussi nel buffer.

Quando un utente cambia il canale e il flusso viene inserito correttamente nel buffer, la chiamata di `play` sul nuovo canale avvia immediatamente la riproduzione.

Sebbene non ci siano limiti al numero di istanze `MediaPlayer` eseguibili da TVSDK, l&#39;esecuzione di più istanze consuma più risorse. Le prestazioni dell&#39;applicazione possono essere influenzate dal numero di istanze in esecuzione. Per ulteriori informazioni su queste istanze, vedere [Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## Configurazione del buffering per la riproduzione istantanea {#configure-buffering-for-instant-on-playback}

Con l&#39;accensione immediata, gli utenti possono cambiare canale e la riproduzione inizia immediatamente senza tempi di attesa. Quando si abilita l’opzione Attivato immediato, TVSDK crea un buffer di uno o più canali prima dell’inizio della riproduzione.

1. Verificare che la risorsa sia stata caricata ed è pronta per la riproduzione verificando che lo stato sia PREPARATO.
1. Prima di chiamare `play`, chiamare `prepareBuffer` per ogni istanza `MediaPlayer`.

   Attiva immediatamente, ovvero TVSDK avvia il buffering senza riprodurre effettivamente la risorsa multimediale. TVSDK invia l&#39;evento `BUFFERING_COMPLETED` quando il buffer è pieno.

   >[!NOTE]
   >
   >Per impostazione predefinita, `prepareBuffer` e `prepareToPlay` impostano il flusso multimediale affinché inizi la riproduzione dall&#39;inizio. Per iniziare da un&#39;altra posizione, passare la posizione (in millisecondi) in `prepareToPlay`.

   ```java
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state,  
                              MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               // By default, prepareToPlay and prepareBuffer buffer and start playing 
               // from the beginning of the stream. To start at another position, 
               // pass it into prepareToPlay. This example starts 5 seconds into the stream. 
               _mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               _mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. Quando ricevete l&#39;evento `BUFFERING_COMPLETE`, avviate la riproduzione dell&#39;elemento o visualizzate un feedback visivo per indicare che il contenuto è completamente incluso nel buffer.

   Se si chiama `play`, la riproduzione deve iniziare immediatamente.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
