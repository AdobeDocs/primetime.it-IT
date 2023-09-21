---
description: TVSDK supporta la ricerca in una posizione specifica (tempo) in cui il flusso è una playlist a finestra scorrevole, sia in streaming video on-demand (VOD) che live.
title: Visualizza una barra di scorrimento di ricerca con la posizione di riproduzione corrente
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Visualizza una barra di scorrimento di ricerca con la posizione di riproduzione corrente{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK supporta la ricerca in una posizione specifica (tempo) in cui il flusso è una playlist a finestra scorrevole, sia in streaming video on-demand (VOD) che live.

>[!IMPORTANT]
>
>La ricerca in uno streaming live è consentita solo per DVR.

1. Imposta i callback per la ricerca.

       La ricerca è asincrona, pertanto TVSDK invia i seguenti eventi correlati alla ricerca:
   
   * `SeekEvent.SEEK_BEGIN` - Ricerca iniziale.
   * `SeekEvent.SEEK_END` - Ricerca riuscita.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` - è stata riregolata la posizione di ricerca fornita dall’utente.

1. Attendi che il lettore sia in uno stato valido per la ricerca.

   Gli stati validi sono READY, COMPLETED, PAUSED e PLAY.

1. Ascolta l’evento appropriato per vedere quando l’utente sta pulendo.
1. Passa la posizione di ricerca richiesta (millisecondi) al `MediaPlayer.seek` metodo.

   ```
   function seek(position:Number):void;
   ```

   Puoi eseguire la ricerca solo nella durata della risorsa ricercabile. Per i video on-demand, la durata è compresa tra 0 e la durata della risorsa.

   >[!TIP]
   >
   >In questo modo la testina di riproduzione viene spostata in una nuova posizione nel flusso, ma la posizione finale calcolata potrebbe differire dalla posizione di ricerca specificata.

1. Attendi che TVSDK invii `SeekEvent.SEEK_END` evento.
1. Recuperate la posizione finale di riproduzione regolata utilizzando event.actualPosition.

       Questo è importante perché la posizione di inizio effettiva dopo la ricerca può essere diversa dalla posizione richiesta. Possono essere applicate diverse regole, tra cui:
   
   * Il comportamento di riproduzione viene influenzato se una ricerca o un altro riposizionamento termina al centro di un’interruzione pubblicitaria o salta un’interruzione pubblicitaria.
   * Se cercate vicino a un limite di segmento, la posizione di ricerca viene regolata all&#39;inizio del segmento.

1. Utilizzare le informazioni sulla posizione quando si visualizza una barra di scorrimento di ricerca.
