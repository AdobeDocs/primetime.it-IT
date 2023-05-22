---
description: Il termine "instant on" (attivazione immediata) si riferisce al precaricamento di uno o più canali, in modo che l’utente che seleziona un canale o cambia canale possa vedere i contenuti riprodotti immediatamente. Il buffering viene già eseguito nel momento in cui l’utente inizia a guardare.
title: Istantanea attiva
exl-id: f640f208-d1b3-467a-be97-38690e10b7ed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Istantanea attiva {#instant-on}

Il termine &quot;instant on&quot; (attivazione immediata) si riferisce al precaricamento di uno o più canali, in modo che l’utente che seleziona un canale o cambia canale possa vedere i contenuti riprodotti immediatamente. Il buffering viene già eseguito nel momento in cui l’utente inizia a guardare.

Senza attivazione immediata, TVSDK inizializza i contenuti multimediali da riprodurre ma non inizia a memorizzare il flusso finché l’applicazione non chiama `play`. L’utente non visualizza alcun contenuto fino al completamento del buffering. Con l’attivazione immediata, puoi avviare più istanze del lettore multimediale (o del caricatore di elementi del lettore multimediale) e TVSDK avvia immediatamente il buffering dei flussi.

Quando un utente cambia il canale e il flusso viene memorizzato nel buffer correttamente, chiama `play` sul nuovo canale avvia immediatamente la riproduzione.

Anche se non ci sono limiti al numero di `MediaPlayer` istanze che TVSDK può eseguire, l&#39;esecuzione di più istanze consuma più risorse. Le prestazioni delle applicazioni possono essere influenzate dal numero di istanze in esecuzione. Per ulteriori informazioni su queste istanze, vedi [Caricare una risorsa multimediale tramite MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## Configurare il buffering per la riproduzione istantanea {#configure-buffering-for-instant-on-playback}

Con l&#39;accensione immediata, gli utenti possono cambiare canale e la riproduzione inizia immediatamente senza tempi di attesa. Quando attivate l&#39;opzione di attivazione immediata, TVSDK esegue il buffer di uno o più canali prima dell&#39;inizio della riproduzione.

1. Verificare che la risorsa sia stata caricata ed è pronta per la riproduzione verificando che lo stato sia PREPARATO.
1. Prima della chiamata `play`, chiama `prepareBuffer` per ogni `MediaPlayer` dell&#39;istanza.

   Questo abilita l’attivazione immediata, il che significa che TVSDK avvia il buffering senza riprodurre effettivamente la risorsa multimediale. TVSDK invia `BUFFERING_COMPLETED` quando il buffer è pieno.

   >[!NOTE]
   >
   >Per impostazione predefinita, `prepareBuffer` e `prepareToPlay` imposta il flusso multimediale per iniziare la riproduzione dall’inizio. Per iniziare da un’altra posizione, passa la posizione (in millisecondi) in `prepareToPlay`.

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

1. Quando ricevi il `BUFFERING_COMPLETE` , avvia la riproduzione dell&#39;elemento o visualizza il feedback visivo per indicare che il contenuto è completamente bufferizzato.

   Se chiami `play`, la riproduzione deve iniziare immediatamente.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
