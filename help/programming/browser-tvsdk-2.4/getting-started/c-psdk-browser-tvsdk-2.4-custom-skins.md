---
description: Per utilizzare le interfacce personalizzate, è necessario scrivere la personalizzazione in modo simile a default-video-Controls.css e fare riferimento a questa nuova personalizzazione nel lettore.
seo-description: Per utilizzare le interfacce personalizzate, è necessario scrivere la personalizzazione in modo simile a default-video-Controls.css e fare riferimento a questa nuova personalizzazione nel lettore.
seo-title: Pelli personalizzate
title: Pelli personalizzate
uuid: bc71926e-0dec-4628-8248-911224a7a6c2
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Pelli personalizzate{#custom-skins}

Per utilizzare le interfacce personalizzate, è necessario scrivere la personalizzazione in modo simile a default-video-Controls.css e fare riferimento a questa nuova personalizzazione nel lettore.

Ad esempio, potete utilizzare una delle seguenti opzioni:

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

Potete apportare i seguenti tipi di modifiche:

* Colore di primo piano dei pulsanti e del testo

   Tutti i controlli in primo piano utilizzano la classe `vid-skin-fgcolor`. Per modificare il primo piano di tutti i controlli, ripetete tutti gli elementi con la classe `vid-skin-fgcolor` e specificate il colore desiderato.
* Colore di sfondo dei pulsanti e del testo

   Tutti i controlli in primo piano utilizzano la classe `vid-skin-bgcolor`. Per modificare il primo piano di tutti i controlli, ripetete tutti gli elementi con la classe `vid-skin-bgcolor` e specificate il colore desiderato.
* Forma della testina di gioco

   La testa di gioco può essere quadrata o rotonda. Per modificare l&#39;indicatore di riproduzione, aggiungere la classe `square` o `round` all&#39;elemento `playhead`.
* Stile dei filetti di tamponamento

   Il lettore di riferimento fornisce i seguenti stili di filetti che possono essere visualizzati come contenuto buffer del lettore:

   * Testo sovrapposto ( `overlay-text`)
   * Spinner rettangolare ( `spinner`)
   * Segnale ( `signal`)
   * Barre verticali ( `vertical`)

      >[!TIP]
      >
      >Per utilizzare uno dei filatori di buffering, è necessario aggiungere la classe nell’elemento buffering-overlay. Ad esempio, per utilizzare `overlay-text`, aggiungere le righe seguenti nel file `BufferOverlay.js`:
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```

