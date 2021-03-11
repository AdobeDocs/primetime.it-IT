---
description: Il termine "istantaneo" si riferisce al precaricamento di uno o più canali in modo che l'utente che seleziona un canale o cambia canale veda il contenuto riprodotto immediatamente. Il buffering viene già eseguito dal momento in cui l’utente inizia a guardare.
title: Instant on
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Istantanea su {#instant-on}

Il termine &quot;istantaneo&quot; si riferisce al precaricamento di uno o più canali in modo che l&#39;utente che seleziona un canale o cambia canale veda il contenuto riprodotto immediatamente. Il buffering viene già eseguito dal momento in cui l’utente inizia a guardare.

Senza l’attivazione immediata, TVSDK inizializza i file multimediali da riprodurre ma non avvia il buffering del flusso fino a quando l’applicazione non chiama `play`. L’utente non visualizza alcun contenuto fino al completamento del buffering. Attivando immediatamente, puoi avviare più istanze di lettori multimediali (o di lettori multimediali) e TVSDK avvia immediatamente il buffering dei flussi.

Quando un utente cambia il canale e il flusso è stato bufferizzato correttamente, la chiamata a `play` sul nuovo canale avvia immediatamente la riproduzione.

Sebbene non ci siano limiti al numero di istanze `MediaPlayer` eseguibili da TVSDK, l&#39;esecuzione di più istanze consuma più risorse. Le prestazioni dell&#39;applicazione possono essere influenzate dal numero di istanze in esecuzione. Per ulteriori informazioni su queste istanze, consulta [Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## Configurare il buffering per la riproduzione istantanea {#configure-buffering-for-instant-on-playback}

Attivando immediatamente, gli utenti possono cambiare canale e la riproduzione inizia immediatamente senza tempi di attesa. Quando si attiva l’accesso immediato, TVSDK carica uno o più canali prima dell’inizio della riproduzione.

1. Conferma che la risorsa sia stata caricata ed è pronta per la riproduzione verificando che lo stato sia PREPARATO.
1. Prima di chiamare `play`, chiama `prepareBuffer` per ogni istanza `MediaPlayer`.

   Ciò consente l’accesso immediato, il che significa che TVSDK avvia il buffering senza riprodurre effettivamente la risorsa multimediale. TVSDK invia l&#39;evento `BUFFERING_COMPLETED` quando il buffer è pieno.

   >[!NOTE]
   >
   >Per impostazione predefinita, `prepareBuffer` e `prepareToPlay` impostano il flusso multimediale per iniziare la riproduzione dall&#39;inizio. Per iniziare da un’altra posizione, passa la posizione (in millisecondi) in `prepareToPlay`.

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

1. Quando ricevi l’evento `BUFFERING_COMPLETE` , inizia a riprodurre l’elemento o visualizza un feedback visivo per indicare che il contenuto è completamente bufferizzato.

   Se si chiama `play`, la riproduzione deve iniziare immediatamente.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
