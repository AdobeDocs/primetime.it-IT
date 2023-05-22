---
title: Inserimento parziale dell’interruzione pubblicitaria
description: Inserimento parziale dell’interruzione pubblicitaria
copied-description: true
exl-id: c86f1e99-7f1e-4a1e-b285-568ad6659f45
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# Inserimento parziale dell’interruzione pubblicitaria {#partial-ad-break-insertion}

Puoi offrire un’esperienza simile alla TV, ovvero poter partecipare a un annuncio in streaming live. La funzione di interruzione annuncio parziale consente di simulare un’esperienza simile a un televisore in cui, se il client avvia uno streaming live all’interno di un midroll, questo inizierà all’interno di tale midroll. È simile al passaggio a un canale TV e gli spot vengono eseguiti senza problemi.

Ad esempio, se un utente si unisce nel mezzo di un’interruzione pubblicitaria di 90 secondi (tre annunci di 30 secondi), 10 secondi nel secondo annuncio (ovvero, a 40 secondi dall’interruzione pubblicitaria), si verifica quanto segue:

* Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguito dal terzo annuncio.
* I tracker degli annunci per l’annuncio parzialmente riprodotto (il secondo annuncio) non vengono attivati. Viene attivato solo il tracker per il terzo annuncio.

Questo comportamento non è abilitato per impostazione predefinita. Per abilitare questa funzione nell’app, effettua le seguenti operazioni:

Attivare la preferenza per l&#39;inserimento parziale dell&#39;interruzione pubblicitaria. Utilizza il nuovo metodo `setPartialAdBreakPref` nell&#39;interfaccia MediaPlayer per attivare questa funzione. Utilizzare `getPartialAdBreakPref` per trovare lo stato corrente di questa preferenza.

```
    MediaPlayer mediaPlayer = new MediaPlayer(getActivity(). getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
```

L’annuncio pre-roll, se disponibile, viene riprodotto, quindi il contenuto viene riprodotto dal punto in diretta, emulando l’esperienza della televisione in diretta.
