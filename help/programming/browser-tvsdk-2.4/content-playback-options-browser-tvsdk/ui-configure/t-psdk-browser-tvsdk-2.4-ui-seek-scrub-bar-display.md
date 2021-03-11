---
description: Nel browser TVSDK, puoi cercare una posizione specifica (tempo) in un flusso. Un flusso può essere una playlist a finestra scorrevole o un contenuto video on demand (VOD).
title: Maniglia ricerca quando si utilizza la barra di ricerca
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Gestisci la ricerca quando utilizzi la barra di ricerca{#handle-seek-when-using-the-seek-bar}

Nel browser TVSDK, puoi cercare una posizione specifica (tempo) in un flusso. Un flusso può essere una playlist a finestra scorrevole o un contenuto video on demand (VOD).

>[!IMPORTANT]
>
>La ricerca in un flusso live è consentita solo per il DVR.

1. Attendi che il TVSDK del browser sia in uno stato valido per la ricerca.

   Gli stati validi sono PREPARATI, COMPLETI, SOSPESI e RIPRODUZIONE. Lo stato valido assicura che la risorsa multimediale sia stata caricata correttamente. Se il lettore non è in uno stato ricercabile valido, il tentativo di chiamare i metodi seguenti genera un `IllegalStateException`.

   Ad esempio, puoi attendere che il browser TVSDK attivi `AdobePSDK.MediaPlayerStatusChangeEvent` con un `event.status` di `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. Passa la posizione di ricerca richiesta al metodo `MediaPlayer.seek` come parametro in millisecondi.

   In questo modo la testina di riproduzione viene spostata in una posizione diversa nel flusso.

   >[!TIP]
   >
   >La posizione di ricerca richiesta potrebbe non coincidere con la posizione effettiva calcolata.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. Attendi che il browser TVSDK attivi l&#39;evento `AdobePSDK.PSDKEventType.SEEK_END` , che restituisce la posizione corretta nell&#39;attributo `actualPosition` dell&#39;evento:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   Questo è importante perché la posizione iniziale effettiva dopo la ricerca potrebbe essere diversa dalla posizione richiesta. Possono essere applicate alcune delle seguenti regole:

   * Il comportamento di riproduzione viene interessato se una ricerca o un altro riposizionamento termina nel mezzo di un&#39;interruzione pubblicitaria o salta interruzioni pubblicitarie.
   * Puoi cercare solo nella durata ricercabile della risorsa. Per il VOD, ossia da 0 alla durata del cespite.

1. Per la barra di ricerca creata nell’esempio precedente, fai clic su `setPositionChangeListener()` per vedere quando l’utente esegue il pulitura:

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

1. Imposta i callback del listener di eventi per le modifiche nell&#39;attività di ricerca dell&#39;utente.

       L&#39;operazione di ricerca è asincrona, quindi il browser TVSDK invia questi eventi relativi alla ricerca:
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` per indicare che la ricerca sta iniziando.
   * `AdobePSDK.PSDKEventType.SEEK_END` per indicare che la ricerca ha avuto successo.
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` per indicare che il lettore multimediale ha modificato la posizione di ricerca fornita dall&#39;utente.

