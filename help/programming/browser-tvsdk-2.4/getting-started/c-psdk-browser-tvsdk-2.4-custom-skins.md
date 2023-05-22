---
description: Per utilizzare gli skin personalizzati, devi scrivere la personalizzazione in modo simile a default-video-controls.css e fare riferimento a questa nuova personalizzazione nel lettore.
title: Interfacce personalizzate
exl-id: 4d627545-942d-4883-a010-afddcffb8dd5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Interfacce personalizzate{#custom-skins}

Per utilizzare gli skin personalizzati, devi scrivere la personalizzazione in modo simile a default-video-controls.css e fare riferimento a questa nuova personalizzazione nel lettore.

Ad esempio, puoi utilizzare una delle seguenti opzioni:

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

Puoi apportare i seguenti tipi di modifiche:

* Colore di primo piano dei pulsanti e del testo

   Tutti i controlli con un primo piano utilizzano `vid-skin-fgcolor` classe. Per modificare il primo piano di tutti i controlli, scorrere tutti gli elementi con `vid-skin-fgcolor` e specificare il colore desiderato.
* Colore di sfondo dei pulsanti e del testo

   Tutti i controlli con un primo piano utilizzano `vid-skin-bgcolor` classe. Per modificare il primo piano di tutti i controlli, scorrere tutti gli elementi con `vid-skin-bgcolor` e specificare il colore desiderato.
* Forma della testina di riproduzione

   La testina di riproduzione può essere quadrata o rotonda. Per cambiare la testina di riproduzione, aggiungi `square` o `round` classe a `playhead` elemento.
* Stile dei filatori di buffering

   Il lettore di riferimento fornisce i seguenti stili di cursori che possono essere visualizzati come contenuto dei buffer del lettore:

   * Testo sovrapposto ( `overlay-text`)
   * Rotellina rettangolare ( `spinner`)
   * Segnale ( `signal`)
   * Barre verticali ( `vertical`)

      >[!TIP]
      >
      >Per utilizzare uno degli spinner di buffering, è necessario aggiungere la classe nell&#39;elemento buffering-overlay. Ad esempio, per utilizzare `overlay-text`, aggiungi le seguenti righe nella `BufferOverlay.js` file:
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```
