---
description: Attivando l'opzione Instant On è possibile precaricare uno o più canali. Quando gli utenti selezionano un canale o cambiano canale, il contenuto viene riprodotto immediatamente. Il buffering è completo per il momento in cui l'utente inizia a guardare.
seo-description: Attivando l'opzione Instant On è possibile precaricare uno o più canali. Quando gli utenti selezionano un canale o cambiano canale, il contenuto viene riprodotto immediatamente. Il buffering è completo per il momento in cui l'utente inizia a guardare.
seo-title: Instant On
title: Instant On
uuid: 5b1ceace-cae7-44c7-b4b9-d45078d58cc3
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Instant On {#instant-on}

Attivando l&#39;opzione Instant On è possibile precaricare uno o più canali. Quando gli utenti selezionano un canale o cambiano canale, il contenuto viene riprodotto immediatamente. Il buffering è completo per il momento in cui l&#39;utente inizia a guardare.

Senza Instant On, TVSDK inizializza il file multimediale da riprodurre ma non avvia il buffering del flusso fino a quando l&#39;applicazione effettua le chiamate `play`. L&#39;utente non vede alcun contenuto fino al completamento del buffering. Con l’opzione Attivato istantaneo, potete avviare più istanze di lettore multimediale (o del caricatore di elementi del lettore multimediale) e TVSDK avvia immediatamente la memorizzazione dei flussi nel buffer. Quando un utente cambia il canale e il flusso viene inserito correttamente nel buffer, la chiamata `play` al nuovo canale avvia immediatamente la riproduzione.

Sebbene non ci siano limiti al numero di istanze `MediaPlayer` `MediaPlayerItemLoader` e istanze eseguibili da TVSDK, l&#39;esecuzione di più istanze consuma più risorse. Le prestazioni dell&#39;applicazione possono essere influenzate dal numero di istanze in esecuzione. Per ulteriori informazioni su `MediaPlayerItemLoader`, consultate [Caricare una risorsa multimediale nel lettore](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md)multimediale.

>[!IMPORTANT]
>
>TVSDK non supporta un singolo `QoSProvider` da utilizzare sia con `itemLoader` che `MediaPlayer`. Se il cliente utilizza Instant On, l&#39;applicazione deve mantenere due istanze QoS e gestire entrambe le istanze per le informazioni.

Per ulteriori informazioni su `MediaPlayerItemLoader`, consultate [Caricare una risorsa multimediale tramite MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Aggiunta di un&#39;istanza del provider QoS a mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Creare e collegare un provider QoS a un&#39; `mediaPlayerItemLoader` istanza

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   Una volta avviata la riproduzione, utilizzate `_qosProvider` per ottenere `timeToLoad` e `timeToPrepare` QoSdata. Le metriche QoS rimanenti possono essere recuperate utilizzando l&#39; `QoSProvider` allegato al `mediaPlayer`.

   Per ulteriori informazioni su `MediaPlayerItemLoader`, consultate [Caricare una risorsa multimediale tramite MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Configurare il buffering per Instant On {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK fornisce metodi e stati per consentire l’utilizzo di Instant On con una risorsa multimediale.

>[!NOTE]
>
>Adobe consiglia di utilizzare `MediaPlayerItemLoader` per InstantOn. Per utilizzare `MediaPlayerItemLoader`anziché `MediaPlayer`, consultare [Caricare una risorsa multimediale tramite MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

1. Verificare che la risorsa sia stata caricata e che il lettore sia pronto a riprodurre la risorsa.
1. Prima di chiamare `play`, chiamare `prepareBuffer` per ogni `MediaPlayer` istanza.

   `prepareBuffer` attiva l’opzione Instant On e TVSDK avvia immediatamente il buffering e invia l’ `BUFFERING_COMPLETED` evento quando il buffer è pieno.

   >[!TIP]
   >
   >Per impostazione predefinita, `prepareBuffer` e `prepareToPlay` impostare il flusso multimediale affinché inizi la riproduzione dall&#39;inizio. Per iniziare da un’altra posizione, passare la posizione (in millisecondi) a `prepareToPlay`.

   ```
   @Override 
   public void onStatusChanged(MediaPlayerStatus status) { 
       switch (status) { 
           case INITIALIZED: 
               // This example starts 5 seconds into the stream. 
               mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. Quando ricevete l’ `BUFFERING_COMPLETE` evento, avviate la riproduzione dell’elemento o visualizzate un feedback visivo per indicare che il contenuto è completamente incluso nel buffer.

   >[!NOTE]
   >
   >Se si chiama `play`, la riproduzione deve iniziare immediatamente.