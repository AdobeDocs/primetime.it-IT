---
description: TVSDK supporta la ricerca di una posizione specifica (tempo) in cui il flusso è una playlist a finestra scorrevole, sia in video on demand (VOD) che in streaming live.
title: Visualizza una barra di scorrimento con la posizione di riproduzione corrente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Visualizza una barra di scorrimento con la posizione di riproduzione corrente{#display-a-seek-scrub-bar-with-the-current-playback-position}

TVSDK supporta la ricerca di una posizione specifica (tempo) in cui il flusso è una playlist a finestra scorrevole, sia in video on demand (VOD) che in streaming live.

>[!IMPORTANT]
>
>La ricerca in un flusso live è consentita solo per il DVR.

1. Imposta i callback per la ricerca.

       La ricerca è asincrona, quindi TVSDK invia i seguenti eventi relativi alla ricerca:
   
   * `SeekEvent.SEEK_BEGIN` - Cercare di iniziare.
   * `SeekEvent.SEEK_END` - Cercare di successo.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` - riadattata la posizione di ricerca fornita dall&#39;utente.

1. Attendi che il lettore sia in uno stato valido per la ricerca.

   Gli stati validi sono PREPARATI, COMPLETATI, SOSPESI E RIPRODUZIONE.

1. Ascoltare l&#39;evento appropriato per vedere quando l&#39;utente esegue il lavaggio.
1. Passa la posizione di ricerca richiesta (millisecondi) al metodo `MediaPlayer.seek` .

   ```
   function seek(position:Number):void;
   ```

   Puoi cercare solo nella durata ricercabile della risorsa. Per i video su richiesta, la durata è compresa tra 0 e la durata della risorsa.

   >[!TIP]
   >
   >In questo modo la testina di riproduzione viene spostata in una nuova posizione nel flusso, ma la posizione calcolata finale potrebbe differire dalla posizione di ricerca specificata.

1. Attendi che TVSDK invii l’evento `SeekEvent.SEEK_END` .
1. Recupera la posizione di riproduzione corretta finale utilizzando event.effectivePosition.

       Questo è importante perché la posizione iniziale effettiva dopo la ricerca può essere diversa dalla posizione richiesta. Possono essere applicate diverse regole, tra cui:
   
   * Il comportamento di riproduzione è interessato se una ricerca o un altro riposizionamento termina al centro di un&#39;interruzione pubblicitaria o salta interruzioni pubblicitarie.
   * Se cerchi vicino a un limite di segmento, la posizione di ricerca viene regolata in base all’inizio del segmento.

1. Utilizza le informazioni sulla posizione quando visualizzi una barra di scorrimento della ricerca.
