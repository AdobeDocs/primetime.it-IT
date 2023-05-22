---
title: Creare un lettore di base utilizzando il Framework dell’interfaccia utente
description: Creare un lettore di base utilizzando il Framework dell’interfaccia utente
copied-description: true
exl-id: 78629042-fd87-406b-af42-229e34d48162
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Creare un lettore di base utilizzando il Framework dell’interfaccia utente{#create-a-basic-player-using-the-ui-framework}

Per creare un lettore di base utilizzando il Framework dell’interfaccia utente:

1. Creare un `<div>` per l’istanza del lettore.

   Ad esempio:

   ```
   <div id="video1" > 
    </div>
   ```

1. Carica il lettore.

   ```js
   <script> 
       (function(){ 
           var player = ptp.videoPlayer('#video1'); 
       })(); 
   </script>
   ```

   Al momento della creazione del lettore, il `<div>` all&#39;elemento viene assegnata una classe CSS di `ptp-main-video-div-style`. Il DOM risultante sarà simile al seguente:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. Aggiungere un controllo UI.

   Ad esempio, aggiungi una barra di controllo che appare quando il mouse passa sopra il lettore:

   ```js
   <script> 
       (function(){ 
           function myControlBarBehavior(element, configuration, player) { 
               return ptp.controlBarBehavior(element, configuration, player); 
           } 
           var player = ptp.videoPlayer('#video1', { 
               controlBar: { 
                   behavior: myControlBarBehavior, 
                   classNames: 'ptp-control-bar my_control_bar' 
               } 
           }); 
       })(); 
   </script>
   ```

   Il DOM risultante viene visualizzato come segue:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <div class="ptp-control-bar my_control_bar"></div> 
       <video class="vp-video-element"></video> 
   </div>
   ```

L&#39;oggetto restituito dalla chiamata `ptp.videoPlayer()` fornisce un comportamento che racchiude l’API del lettore multimediale TVSDK e consente il controllo programmatico della riproduzione. Quando effettui chiamate sull’istanza del lettore multimediale, l’interfaccia utente si aggiorna in base agli eventi attivati dal lettore multimediale:

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
