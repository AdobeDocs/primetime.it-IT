---
title: Inserimento di interruzioni pubblicitarie parziali
description: Inserimento di interruzioni pubblicitarie parziali
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# Inserimento di interruzioni pubblicitarie parziali {#partial-ad-break-insertion}

È possibile abilitare un&#39;esperienza simile a quella televisiva di essere in grado di partecipare nel mezzo di un annuncio, in flussi live. La funzione di interruzione dell’annuncio parziale consente di imitare un’esperienza simile a quella televisiva in cui, se il cliente avvia un flusso live all’interno di un proxy, questo verrà avviato all’interno di tale proxy. È simile al passaggio a un canale televisivo e gli spot vengono eseguiti senza problemi.

Ad esempio, se un utente si unisce nel mezzo di un’interruzione pubblicitaria di 90 secondi (tre annunci di 30 secondi), a 10 secondi dalla seconda inserzione (cioè a 40 secondi dall’interruzione pubblicitaria), si verifica quanto segue:

* Il secondo annuncio viene riprodotto per la durata rimanente (20 sec) seguita dal terzo annuncio.
* I tracciatori di annunci per l’annuncio parzialmente riprodotto (il secondo annuncio) non vengono attivati. Viene attivato solo il tracker per il terzo annuncio.

Questo comportamento non è abilitato per impostazione predefinita. Per abilitare questa funzione nell’app, procedi come segue:

1. Disattiva i record live utilizzando il metodo setEnableLivePreroll della classe AdvertisingMetadata.

   ```
   advertisingMetadata.setLivePreroll(false)  
   advertisingMetadata.setPreroll(false)
   ```

1. Attiva la preferenza per l’inserimento di interruzioni pubblicitarie parziali. Utilizza il nuovo metodo setPartialAdBreakPref nell&#39;interfaccia MediaPlayer per attivare questa funzione. Utilizzare il metodo getPartialAdBreakPref per trovare lo stato corrente di questa preferenza.

   ```
   MediaPlayer mediaPlayer = new MediaPlayer(getActivity().getApplicationContext()); 
    mediaPlayer.setPartialAdBreakPref(true);
   ```

