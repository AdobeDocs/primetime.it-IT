---
description: Per utilizzare gli skin personalizzati, è necessario scrivere la personalizzazione simile a default-video-Controls.css e fare riferimento a questa nuova personalizzazione nel lettore.
title: Pelli personalizzate
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# Pelli personalizzate{#custom-skins}

Per utilizzare gli skin personalizzati, è necessario scrivere la personalizzazione simile a default-video-Controls.css e fare riferimento a questa nuova personalizzazione nel lettore.

Ad esempio, puoi utilizzare una delle seguenti opzioni:

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

Puoi effettuare i seguenti tipi di modifiche:

* Colore di primo piano dei pulsanti e del testo

   Tutti i controlli in primo piano utilizzano la classe `vid-skin-fgcolor` . Per modificare il primo piano di tutti i controlli, eseguire l&#39;iterazione di tutti gli elementi con la classe `vid-skin-fgcolor` e specificare il colore desiderato.
* Colore di sfondo dei pulsanti e del testo

   Tutti i controlli in primo piano utilizzano la classe `vid-skin-bgcolor` . Per modificare il primo piano di tutti i controlli, eseguire iterazioni su tutti gli elementi con la classe `vid-skin-bgcolor` e specificare il colore desiderato.
* Forma della testina di gioco

   La testa di gioco può essere quadrata o rotonda. Per modificare la testina di riproduzione, aggiungere la classe `square` o `round` all&#39;elemento `playhead`.
* Stile dei filetti di buffering

   Il lettore di riferimento fornisce i seguenti stili di spinaroli che possono essere visualizzati come contenuto del buffer del lettore:

   * Testo sovrapposto ( `overlay-text`)
   * Spinner rettangolare ( `spinner`)
   * Segnale ( `signal`)
   * Barre verticali ( `vertical`)

      >[!TIP]
      >
      >Per utilizzare uno qualsiasi degli spinatori di buffering, devi aggiungere la classe nell’elemento di buffering-overlay. Ad esempio, per utilizzare `overlay-text`, aggiungi le seguenti righe nel file `BufferOverlay.js` :
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```

