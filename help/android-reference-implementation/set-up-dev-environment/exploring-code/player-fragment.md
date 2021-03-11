---
description: La classe PlayerFragment è il luogo in cui si modifica il codice per creare i gestori di funzioni completamente abilitati.
title: PlayerFragment
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# PlayerFragment {#playerfragment}

La classe PlayerFragment è il luogo in cui si modifica il codice per creare i gestori di funzioni completamente abilitati.

La classe `PlayerFragment` contiene tutti i componenti dell&#39;interfaccia utente quali `playerFrame`, `ControlBar`, `playerClickableAdFragment` e `adOverlay`.

Gestisce l’inizializzazione di tutti questi componenti, nonché la creazione del lettore, l’impostazione delle visualizzazioni, la creazione di gestori di funzioni per il lettore multimediale, la gestione di eventi multimediali come la ripresa, la riproduzione e la pausa e la gestione degli ascoltatori di eventi per `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager` e `EntitlementManager`.

Il file XML che include i parametri di configurazione per `PlayerFragment` è `res/layout/fragment_player.xml`.

Prima di creare i gestori di funzioni è necessario creare il lettore multimediale assicurandosi che il seguente codice sia nel file `PlayerFragment.java` :

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
