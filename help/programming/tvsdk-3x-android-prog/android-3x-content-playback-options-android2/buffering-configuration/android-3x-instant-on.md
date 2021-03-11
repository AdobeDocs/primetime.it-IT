---
description: Attivando l'opzione Immediato si precarica uno o più canali. Quando gli utenti selezionano un canale o passano a un altro canale, il contenuto viene riprodotto immediatamente. Il buffering viene completato dal momento in cui l’utente inizia a guardare.
title: Instant On
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Instant On {#instant-on}

Attivando l&#39;opzione Immediato si precarica uno o più canali. Quando gli utenti selezionano un canale o passano a un altro canale, il contenuto viene riprodotto immediatamente. Il buffering viene completato dal momento in cui l’utente inizia a guardare.

Senza Instant On, TVSDK inizializza i file multimediali da riprodurre ma non avvia il buffering del flusso fino a quando l&#39;applicazione non chiama `play`. L’utente non visualizza alcun contenuto fino al completamento del buffering. Con Instant On, è possibile avviare più istanze del lettore multimediale (o del caricatore di elementi del lettore multimediale) e TVSDK avvia immediatamente il buffering dei flussi. Quando un utente cambia il canale e il flusso è stato bufferizzato correttamente, la chiamata a `play` sul nuovo canale avvia immediatamente la riproduzione.

Sebbene non vi siano limiti al numero di istanze `MediaPlayer` e `MediaPlayerItemLoader` eseguibili da TVSDK, l&#39;esecuzione di più istanze consuma più risorse. Le prestazioni dell&#39;applicazione possono essere influenzate dal numero di istanze in esecuzione. Per ulteriori informazioni su `MediaPlayerItemLoader`, consulta [Caricare una risorsa multimediale nel lettore multimediale](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK non supporta un singolo `QoSProvider` per funzionare sia con `itemLoader` che con `MediaPlayer`. Se il cliente utilizza Instant On, l&#39;applicazione deve mantenere due istanze QoS e gestire entrambe le istanze per le informazioni.

Per ulteriori informazioni su `MediaPlayerItemLoader`, consulta [Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Aggiungi un&#39;istanza del provider QoS a mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Crea e allega un provider QoS a un&#39;istanza `mediaPlayerItemLoader`

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   Una volta avviata la riproduzione, utilizzare `_qosProvider` per ottenere `timeToLoad` e `timeToPrepare` QoSdata. Le metriche QoS rimanenti possono essere recuperate utilizzando il tag `QoSProvider` associato al tag `mediaPlayer`.

   Per ulteriori informazioni su `MediaPlayerItemLoader`, consulta [Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Configurare il buffering per Instant On {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK fornisce metodi e stati per consentire l’utilizzo di Instant On con una risorsa multimediale.

>[!NOTE]
>
>Adobe consiglia di utilizzare `MediaPlayerItemLoader` per InstantOn. Per utilizzare `MediaPlayerItemLoader` anziché `MediaPlayer`, vedere [Caricare una risorsa multimediale utilizzando MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

1. Conferma che la risorsa sia stata caricata e che il lettore sia pronto a riprodurre la risorsa.
1. Prima di chiamare `play`, chiama `prepareBuffer` per ogni istanza `MediaPlayer`.

   `prepareBuffer` abilita Instant On e TVSDK avvia immediatamente il buffering e invia l&#39; `BUFFERING_COMPLETED` evento quando il buffer è pieno.

   >[!TIP]
   >
   >Per impostazione predefinita, `prepareBuffer` e `prepareToPlay` impostano il flusso multimediale per iniziare la riproduzione dall&#39;inizio. Per iniziare da un’altra posizione, passa la posizione (in millisecondi) a `prepareToPlay`.

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

1. Quando ricevi l’evento `BUFFERING_COMPLETE` , inizia a riprodurre l’elemento o visualizza un feedback visivo per indicare che il contenuto è completamente bufferizzato.

   >[!NOTE]
   >
   >Se si chiama `play`, la riproduzione deve iniziare immediatamente.