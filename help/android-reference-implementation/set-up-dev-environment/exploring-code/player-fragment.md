---
description: La classe PlayerFragment è il punto in cui si modifica il codice per creare i gestori di funzioni completamente abilitati.
seo-description: La classe PlayerFragment è il punto in cui si modifica il codice per creare i gestori di funzioni completamente abilitati.
seo-title: PlayerFragment
title: PlayerFragment
uuid: 83f02c31-f3b1-4d16-97c8-5b391e8c999a
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---


# PlayerFragment {#playerfragment}

La classe PlayerFragment è il punto in cui si modifica il codice per creare i gestori di funzioni completamente abilitati.

La classe `PlayerFragment` contiene tutti i componenti dell&#39;interfaccia utente quali `playerFrame`, `ControlBar`, `playerClickableAdFragment` e `adOverlay`.

Gestisce l&#39;inizializzazione di tutti questi componenti, oltre a creare il lettore, configurare le viste, creare i manager delle funzioni per il lettore multimediale, gestire eventi multimediali come la ripresa, la riproduzione e la pausa e gestire i listener di eventi per `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager` e `EntitlementManager`.

Il file XML che include i parametri di configurazione per `PlayerFragment` è `res/layout/fragment_player.xml`.

Prima di creare i feature manager è necessario creare il lettore multimediale verificando che il seguente codice sia nel file `PlayerFragment.java`:

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
