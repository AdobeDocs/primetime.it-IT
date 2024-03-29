---
description: L'attivazione immediata comporta il precaricamento di uno o più canali. Quando gli utenti selezionano un canale o cambiano canale, il contenuto viene riprodotto immediatamente. Il buffering viene completato nel momento in cui l’utente inizia a guardare.
title: Istantanea attiva
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Istantanea attiva {#instant-on}

L&#39;attivazione immediata comporta il precaricamento di uno o più canali. Quando gli utenti selezionano un canale o cambiano canale, il contenuto viene riprodotto immediatamente. Il buffering viene completato nel momento in cui l’utente inizia a guardare.

Senza Instant On, TVSDK inizializza il contenuto multimediale da riprodurre ma non inizia a memorizzare il flusso fino a quando l&#39;applicazione non chiama `play`. L’utente non visualizza alcun contenuto fino al completamento del buffering. Con Instant On, puoi avviare più istanze del lettore multimediale (o del caricatore di elementi del lettore multimediale) e TVSDK avvia immediatamente il buffering dei flussi. Quando un utente cambia il canale e il flusso viene memorizzato nel buffer correttamente, chiama `play` sul nuovo canale avvia immediatamente la riproduzione.

Anche se non ci sono limiti al numero di `MediaPlayer` e `MediaPlayerItemLoader` istanze che TVSDK può eseguire, l&#39;esecuzione di più istanze consuma più risorse. Le prestazioni delle applicazioni possono essere influenzate dal numero di istanze in esecuzione. Per ulteriori informazioni su `MediaPlayerItemLoader`, vedi [Caricare una risorsa multimediale nel lettore multimediale](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

>[!IMPORTANT]
>
>TVSDK non supporta un `QoSProvider` per lavorare con entrambi `itemLoader` e `MediaPlayer`. Se il cliente utilizza Instant On, l’applicazione deve mantenere due istanze QoS e gestire entrambe le istanze per le informazioni.

Per ulteriori informazioni su `MediaPlayerItemLoader`, vedi [Caricare una risorsa multimediale tramite MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Aggiungere un’istanza del provider QoS a mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Creare e collegare un provider QoS a un `mediaPlayerItemLoader` istanza

  ```
  // Create an instance of QoSProvider  
  private QOSProvider _qosProvider = new QOSProvider(this._context);  
  
  // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
  // (before calling load API on mediaPlayerItemLoader instance)  
  _qosProvider.attachMediaPlayerItemLoader(this._loader); 
  ```

  Una volta avviata la riproduzione, utilizzare `_qosProvider` per ottenere `timeToLoad` e `timeToPrepare` QoSdata. Le metriche QoS rimanenti possono essere recuperate utilizzando `QoSProvider` collegato al `mediaPlayer`.

  Per ulteriori informazioni su `MediaPlayerItemLoader`, vedi [Caricare una risorsa multimediale tramite MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Configurare il buffering per Instant On {#section_4FE346B7BE434BA8A2203896D6E52146}

TVSDK fornisce metodi e stati per consentire l&#39;utilizzo di Instant On con una risorsa multimediale.

>[!NOTE]
>
>L’Adobe consiglia di utilizzare `MediaPlayerItemLoader` per InstantOn. Da utilizzare `MediaPlayerItemLoader`, anziché `MediaPlayer`, vedi [Caricare una risorsa multimediale tramite MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

1. Verifica che la risorsa sia stata caricata e che il lettore sia preparato per riprodurla.
1. Prima della chiamata `play`, chiama `prepareBuffer` per ogni `MediaPlayer` dell&#39;istanza.

   `prepareBuffer` attiva l&#39;attivazione immediata e TVSDK avvia immediatamente il buffering e invia il `BUFFERING_COMPLETED` quando il buffer è pieno.

   >[!TIP]
   >
   >Per impostazione predefinita, `prepareBuffer` e `prepareToPlay` imposta il flusso multimediale per iniziare la riproduzione dall’inizio. Per iniziare da un’altra posizione, passa la posizione (in millisecondi) a `prepareToPlay`.

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

1. Quando ricevi il `BUFFERING_COMPLETE` , avvia la riproduzione dell&#39;elemento o visualizza il feedback visivo per indicare che il contenuto è completamente bufferizzato.

   >[!NOTE]
   >
   >Se chiami `play`, la riproduzione deve iniziare immediatamente.
