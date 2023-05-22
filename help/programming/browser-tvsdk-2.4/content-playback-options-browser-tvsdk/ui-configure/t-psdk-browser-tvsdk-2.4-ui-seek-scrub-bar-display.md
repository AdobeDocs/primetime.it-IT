---
description: In Browser TVSDK, puoi cercare una posizione specifica (ora) in un flusso. Un flusso può essere una playlist a finestra scorrevole o un contenuto video-on-demand (VOD).
title: Gestire la ricerca quando si utilizza la barra di ricerca
exl-id: 4c09b218-917a-4318-82b0-c221d450a2c1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Gestire la ricerca quando si utilizza la barra di ricerca{#handle-seek-when-using-the-seek-bar}

In Browser TVSDK, puoi cercare una posizione specifica (ora) in un flusso. Un flusso può essere una playlist a finestra scorrevole o un contenuto video-on-demand (VOD).

>[!IMPORTANT]
>
>La ricerca in uno streaming live è consentita solo per DVR.

1. Attendi che il browser TVSDK sia in uno stato valido per la ricerca.

   Gli stati validi sono READY, COMPLETE, PAUSED e PLAY. Lo stato di validità garantisce che la risorsa multimediale sia stata caricata correttamente. Se il lettore non si trova in uno stato valido ricercabile, il tentativo di chiamare i metodi seguenti genera un `IllegalStateException`.

   Ad esempio, puoi aspettare che TVSDK del browser attivi  `AdobePSDK.MediaPlayerStatusChangeEvent`  con un `event.status` di `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. Passa la posizione di ricerca richiesta a `MediaPlayer.seek` come parametro in millisecondi.

   In questo modo la testina di riproduzione viene spostata in una posizione diversa nel flusso.

   >[!TIP]
   >
   >La posizione di ricerca richiesta potrebbe non coincidere con la posizione calcolata effettiva.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. Attendere che TVSDK del browser attivi  `AdobePSDK.PSDKEventType.SEEK_END`  , che restituisce la posizione regolata nel `actualPosition` attributo:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   Questo è importante perché la posizione di inizio effettiva dopo la ricerca potrebbe essere diversa dalla posizione richiesta. Potrebbero essere applicabili alcune delle seguenti regole:

   * Il comportamento di riproduzione viene modificato se una ricerca o un altro riposizionamento termina al centro di un’interruzione pubblicitaria o salta un’interruzione pubblicitaria.
   * Puoi eseguire la ricerca solo nella durata della risorsa ricercabile. Per VOD, è compreso tra 0 e la durata della risorsa.

1. Per la barra di ricerca creata nell’esempio precedente, ascolta `setPositionChangeListener()` per vedere quando l’utente sta pulendo:

   ```js
   seekBar.setPositionChangeListener(function (pos) { 
                   var range = player.seekableRange; 
                   if (range) { 
                       var duration = range.duration; 
                       var time = duration * pos; // seek bar range is [0,1] 
                       player.seek(time); 
   
                       console.log("seek to " + time + " / " + duration); 
                   } 
   
               }); 
   ```

1. Configurare i callback del listener di eventi per le modifiche nell&#39;attività di ricerca dell&#39;utente.

       L’operazione di ricerca è asincrona, pertanto il TVSDK del browser invia questi eventi relativi alla ricerca:
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` per indicare l&#39;avvio della ricerca.
   * `AdobePSDK.PSDKEventType.SEEK_END` per indicare che la ricerca è stata eseguita correttamente.
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` per indicare che il lettore multimediale ha regolato nuovamente la posizione di ricerca fornita dall’utente.
