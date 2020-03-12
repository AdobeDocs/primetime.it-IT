---
description: La classe PlayerFragment è il punto in cui si modifica il codice per creare i gestori di funzioni completamente abilitati.
seo-description: La classe PlayerFragment è il punto in cui si modifica il codice per creare i gestori di funzioni completamente abilitati.
seo-title: PlayerFragment
title: PlayerFragment
uuid: 83f02c31-f3b1-4d16-97c8-5b391e8c999a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# PlayerFragment {#playerfragment}

La classe PlayerFragment è il punto in cui si modifica il codice per creare i gestori di funzioni completamente abilitati.

La `PlayerFragment` classe contiene tutti i componenti dell&#39;interfaccia utente quali `playerFrame`, `ControlBar`, `playerClickableAdFragment`e `adOverlay`.

Gestisce l’inizializzazione di tutti questi componenti, nonché la creazione del lettore, l’impostazione delle viste, la creazione di feature manager per il lettore multimediale, la gestione di eventi multimediali come la ripresa, la riproduzione e la pausa e la gestione dei listener di eventi per `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager`e `EntitlementManager`.

Il file XML che include i parametri di configurazione per il file `PlayerFragment` è `res/layout/fragment_player.xml`.

Prima di creare i feature manager è necessario creare il lettore multimediale verificando che nel `PlayerFragment.java` file sia presente il seguente codice:

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
