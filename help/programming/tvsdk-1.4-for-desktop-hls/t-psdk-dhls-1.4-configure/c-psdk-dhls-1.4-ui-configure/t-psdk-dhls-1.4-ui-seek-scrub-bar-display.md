---
description: TVSDK supporta la ricerca di una posizione (ora) specifica in cui il flusso è una playlist con finestra scorrevole, sia nei flussi video on demand (VOD) che in quelli live.
seo-description: TVSDK supporta la ricerca di una posizione (ora) specifica in cui il flusso è una playlist con finestra scorrevole, sia nei flussi video on demand (VOD) che in quelli live.
seo-title: Visualizzare una barra di scorrimento della ricerca con la posizione di riproduzione corrente
title: Visualizzare una barra di scorrimento della ricerca con la posizione di riproduzione corrente
uuid: f940b305-4893-4531-9a79-53670f5fd23f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Visualizzare una barra di scorrimento della ricerca con la posizione di riproduzione corrente{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK supporta la ricerca di una posizione (ora) specifica in cui il flusso è una playlist con finestra scorrevole, sia nei flussi video on demand (VOD) che in quelli live.

>[!IMPORTANT]
>
>La ricerca in un flusso live è consentita solo per il DVR.

1. Configurare le callback per la ricerca.

       La ricerca è asincrona, pertanto TVSDK invia i seguenti eventi relativi alla ricerca:
   
   * `SeekEvent.SEEK_BEGIN` - Cercare di iniziare.
   * `SeekEvent.SEEK_END` - Cercare di successo.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` - ha regolato la posizione di ricerca fornita dall&#39;utente.

1. Attendere che il lettore sia in uno stato valido per la ricerca.

   Gli stati validi sono PREPARATI, COMPLETATI, SOSPESI E RIPRODUZIONE.

1. Ascoltare l’evento appropriato per visualizzare quando l’utente sta eseguendo il trascinamento.
1. Passa la posizione di ricerca richiesta (millisecondi) al `MediaPlayer.seek` metodo.

   ```
   function seek(position:Number):void;
   ```

   Potete effettuare ricerche solo nella durata della risorsa. Per i video su richiesta, la durata è compresa tra 0 e la durata della risorsa.

   >[!TIP]
   >
   >In questo modo la testina di riproduzione si sposta in una nuova posizione nel flusso, ma la posizione calcolata finale potrebbe essere diversa dalla posizione di ricerca specificata.

1. Attendi che TVSDK invii l&#39; `SeekEvent.SEEK_END` evento.
1. Recuperate la posizione di riproduzione rettificata finale utilizzando event.effectivePosition.

       Questo è importante perché la posizione iniziale effettiva dopo la ricerca può essere diversa dalla posizione richiesta. Possono essere applicate varie regole, tra cui:
   
   * Il comportamento di riproduzione è interessato se una ricerca o un altro riposizionamento termina al centro di un&#39;interruzione di annuncio o salta le interruzioni di annuncio.
   * Se si cerca vicino al limite di un segmento, la posizione di ricerca viene regolata all&#39;inizio del segmento.

1. Utilizzate le informazioni sulla posizione quando visualizzate una barra di scorrimento della ricerca.
