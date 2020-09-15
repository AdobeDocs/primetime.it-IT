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

   Tutti i controlli in primo piano utilizzano la `vid-skin-fgcolor` classe. Per modificare il primo piano di tutti i controlli, ripetete tutti gli elementi con la `vid-skin-fgcolor` classe e specificate il colore desiderato.
* Colore di sfondo dei pulsanti e del testo

   Tutti i controlli con un primo piano utilizzano la `vid-skin-bgcolor` classe. Per modificare il primo piano di tutti i controlli, ripetete tutti gli elementi con `vid-skin-bgcolor` classe e specificate il colore desiderato.
* Forma della testina di gioco

   La testa di gioco può essere quadrata o rotonda. Per cambiare l&#39;indicatore di riproduzione, aggiungete `square` o `round` la classe all&#39; `playhead` elemento.
* Stile dei filetti di tamponamento

   Il lettore di riferimento fornisce i seguenti stili di filetti che possono essere visualizzati come contenuto buffer del lettore:

   * Sovrapposizione testo ( `overlay-text`)
   * Spinner rettangolare ( `spinner`)
   * Segnale ( `signal`)
   * Barre verticali ( `vertical`)

      >[!TIP]
      >
      >Per utilizzare uno dei filatori di buffering, è necessario aggiungere la classe nell’elemento buffering-overlay. Ad esempio, per utilizzare `overlay-text`, aggiungere le righe seguenti nel `BufferOverlay.js` file:
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```

