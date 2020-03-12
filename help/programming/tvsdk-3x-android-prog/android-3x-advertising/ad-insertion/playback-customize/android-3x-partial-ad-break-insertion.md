---
description: 'null'
seo-description: 'null'
seo-title: Inserimento interruzione annuncio parziale
title: Inserimento interruzione annuncio parziale
uuid: a81295b8-77fe-4475-a472-080ee7804d7a
translation-type: tm+mt
source-git-commit: fe9d7d1b2b23a70eb4e212de3d9bda47fc11d8f1

---


# Inserimento Parziale Ad-break {#partial-ad-break-insertion}

Potete abilitare un&#39;esperienza simile a quella televisiva per partecipare nel mezzo di un annuncio, in streaming live. La funzione di interruzione annuncio parziale consente di simulare un&#39;esperienza simile a quella di un televisore in cui, se il cliente avvia un flusso live all&#39;interno di un midroll, questo verrà avviato all&#39;interno di tale midrol. È simile al passaggio a un canale TV e la pubblicità funziona senza problemi.

Ad esempio, se un utente si unisce al centro di un annuncio pubblicitario di 90 secondi (tre annunci da 30 secondi), 10 secondi alla seconda pubblicità (ovvero, a 40 secondi dall&#39;interruzione dell&#39;annuncio), si verifica quanto segue:

* Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguita dal terzo annuncio.
* I tracciatori di annunci per l&#39;annuncio parzialmente riprodotto (il secondo annuncio) non vengono attivati. Viene attivato solo il tracciatore del terzo annuncio.

Questo comportamento non è attivato per impostazione predefinita. Per abilitare questa funzione nell&#39;app, effettua le seguenti operazioni:

Attivate la preferenza per l&#39;inserimento di interruzioni pubblicitarie parziali. Utilizzate il nuovo metodo `setPartialAdBreakPref` nell’interfaccia di MediaPlayer per attivare questa funzione. Utilizzare `getPartialAdBreakPref` il metodo per trovare lo stato corrente di questa preferenza.

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

L&#39;annuncio pre-roll, se disponibile, viene riprodotto, e poi il contenuto viene riprodotto dal punto in diretta emulando l&#39;esperienza della televisione in diretta.
