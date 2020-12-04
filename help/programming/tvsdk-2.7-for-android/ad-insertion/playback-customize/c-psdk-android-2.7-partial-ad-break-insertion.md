---
description: 'null'
seo-description: 'null'
seo-title: Inserimento interruzione annuncio parziale
title: Inserimento interruzione annuncio parziale
uuid: cc071c89-f813-419e-a2b2-4f6a9fdccd6a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Inserimento interruzione annuncio parziale {#partial-ad-break-insertion}

Potete abilitare un&#39;esperienza simile a quella televisiva per partecipare nel mezzo di un annuncio, in streaming live. La funzione di interruzione annuncio parziale consente di simulare un&#39;esperienza simile a quella di un televisore in cui, se il cliente avvia un flusso live all&#39;interno di un midroll, questo verrà avviato all&#39;interno di tale midrol. È simile al passaggio a un canale TV e la pubblicità funziona senza problemi.

Ad esempio, se un utente si unisce al centro di un annuncio pubblicitario di 90 secondi (tre annunci da 30 secondi), 10 secondi alla seconda pubblicità (ovvero, a 40 secondi dall&#39;interruzione dell&#39;annuncio), si verifica quanto segue:

* Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguita dal terzo annuncio.
* I tracciatori di annunci per l&#39;annuncio parzialmente riprodotto (il secondo annuncio) non vengono attivati. Viene attivato solo il tracciatore del terzo annuncio.

Questo comportamento non è attivato per impostazione predefinita. Per abilitare questa funzione nell&#39;app, effettua le seguenti operazioni:

1. Disattivate i primi dinamici utilizzando il metodo setEnableLivePreroll della classe AdvertisingMetadata.

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. Attivate la preferenza per l&#39;inserimento di interruzioni pubblicitarie parziali. Utilizzare il nuovo metodo setPartialAdBreakPref nell&#39;interfaccia di MediaPlayer per attivare questa funzione. Utilizzare il metodo getPartialAdBreakPref per trovare lo stato corrente di questa preferenza.

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```

