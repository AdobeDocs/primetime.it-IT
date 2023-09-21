---
title: Inserimento parziale dell’interruzione pubblicitaria
description: Inserimento parziale dell’interruzione pubblicitaria
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Inserimento parziale dell’interruzione pubblicitaria {#partial-ad-break-insertion}

Puoi offrire un’esperienza simile alla TV, ovvero poter partecipare a un annuncio in streaming live. La funzione di interruzione annuncio parziale consente di simulare un’esperienza simile a un televisore in cui, se il client avvia uno streaming live all’interno di un midroll, questo inizierà all’interno di tale midroll. È simile al passaggio a un canale TV e gli spot vengono eseguiti senza problemi.

Ad esempio, se un utente si unisce nel mezzo di un’interruzione pubblicitaria di 90 secondi (tre annunci di 30 secondi), 10 secondi nel secondo annuncio (ovvero, a 40 secondi dall’interruzione pubblicitaria), si verifica quanto segue:

* Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguito dal terzo annuncio.
* I tracker degli annunci per l’annuncio parzialmente riprodotto (il secondo annuncio) non vengono attivati. Viene attivato solo il tracker per il terzo annuncio.

Questo comportamento non è abilitato per impostazione predefinita. Per abilitare questa funzione nell’app, effettua le seguenti operazioni:

1. Disattiva i preroll attivi utilizzando il metodo setEnableLivePreroll della classe AdvertisingMetadata.

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. Attivare la preferenza per l&#39;inserimento parziale dell&#39;interruzione pubblicitaria. Utilizzare il nuovo metodo setPartialAdBreakPref nell&#39;interfaccia MediaPlayer per attivare questa funzione. Utilizzare il metodo getPartialAdBreakPref per trovare lo stato corrente di questa preferenza.

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```
