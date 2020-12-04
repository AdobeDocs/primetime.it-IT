---
description: Nel browser TVSDK, puoi cercare una posizione specifica (tempo) in un flusso. Un flusso può essere una playlist con finestra scorrevole o un contenuto video su richiesta (VOD).
seo-description: Nel browser TVSDK, puoi cercare una posizione specifica (tempo) in un flusso. Un flusso può essere una playlist con finestra scorrevole o un contenuto video su richiesta (VOD).
seo-title: Gestire la ricerca quando si utilizza la barra di ricerca
title: Gestire la ricerca quando si utilizza la barra di ricerca
uuid: a7c74141-581f-40a3-9d28-ce56ba56773c
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# Ricerca manuale quando si utilizza la barra di ricerca{#handle-seek-when-using-the-seek-bar}

Nel browser TVSDK, puoi cercare una posizione specifica (tempo) in un flusso. Un flusso può essere una playlist con finestra scorrevole o un contenuto video su richiesta (VOD).

>[!IMPORTANT]
>
>La ricerca in un flusso live è consentita solo per il DVR.

1. Attendete che il TVSDK del browser sia in uno stato valido per la ricerca.

   Gli stati validi sono PREPARATI, COMPLETI, SOSPESI E RIPRODUZIONE. Lo stato valido assicura che la risorsa multimediale sia stata caricata correttamente. Se il lettore non è in uno stato ricercabile valido, il tentativo di chiamare i seguenti metodi genera un `IllegalStateException`.

   Ad esempio, è possibile attendere che il browser TVSDK attivi `AdobePSDK.MediaPlayerStatusChangeEvent` con un `event.status` di `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. Passa la posizione di ricerca richiesta al metodo `MediaPlayer.seek` come parametro, in millisecondi.

   In questo modo la testina di riproduzione si sposta in una posizione diversa nello streaming.

   >[!TIP]
   >
   >La posizione di ricerca richiesta potrebbe non coincidere con la posizione effettiva calcolata.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. Attendete che l&#39;SDK del browser attivi l&#39;evento `AdobePSDK.PSDKEventType.SEEK_END`, che restituisce la posizione corretta nell&#39;attributo `actualPosition` dell&#39;evento:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   Questo è importante perché la posizione iniziale effettiva dopo la ricerca potrebbe essere diversa dalla posizione richiesta. Possono essere applicate alcune delle seguenti regole:

   * Il comportamento di riproduzione è interessato dal fatto che una ricerca, o un altro riposizionamento, termina al centro di un&#39;interruzione dell&#39;annuncio o salta le interruzioni dell&#39;annuncio.
   * Potete effettuare ricerche solo nella durata della risorsa. Per il VOD, ossia da 0 alla durata della risorsa.

1. Per la barra di ricerca creata nell&#39;esempio precedente, ascoltate `setPositionChangeListener()` per vedere quando l&#39;utente sta eseguendo il trascinamento:

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

1. Impostare le callback del listener di eventi per le modifiche nell&#39;attività di ricerca dell&#39;utente.

       L&#39;operazione di ricerca è asincrona, pertanto Browser TVSDK invia questi eventi relativi alla ricerca:
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` per indicare l&#39;avvio della ricerca.
   * `AdobePSDK.PSDKEventType.SEEK_END` per indicare che la ricerca ha avuto successo.
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` per indicare che il lettore multimediale ha regolato la posizione di ricerca fornita dall&#39;utente.

