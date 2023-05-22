---
description: La classe PlayerFragment è il luogo in cui si modifica il codice per creare i gestori di funzioni completamente abilitati.
title: PlayerFragment
exl-id: 9060f0f5-9148-48cd-b89b-718607dd70bc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# PlayerFragment {#playerfragment}

La classe PlayerFragment è il luogo in cui si modifica il codice per creare i gestori di funzioni completamente abilitati.

Il `PlayerFragment` La classe contiene tutti i componenti dell&#39;interfaccia utente, ad esempio `playerFrame`, `ControlBar`, `playerClickableAdFragment`, e `adOverlay`.

Gestisce l’inizializzazione di tutti questi componenti, nonché la creazione del lettore, la configurazione delle visualizzazioni, la creazione di gestori di funzionalità per il lettore multimediale, la gestione di eventi multimediali come la ripresa, la riproduzione, la pausa e la gestione dei listener di eventi per `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager`, e `EntitlementManager`.

Il file XML che include i parametri di configurazione per `PlayerFragment` è `res/layout/fragment_player.xml`.

Prima di creare i gestori delle funzioni, è necessario creare il lettore multimediale verificando che nel `PlayerFragment.java` file:

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
