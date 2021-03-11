---
title: Creare un lettore di base utilizzando il framework dell'interfaccia utente
description: Creare un lettore di base utilizzando il framework dell'interfaccia utente
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 1%

---


# Crea un lettore di base utilizzando l&#39;interfaccia utente Framework{#create-a-basic-player-using-the-ui-framework}

Per creare un lettore di base utilizzando il framework dell&#39;interfaccia utente:

1. Crea un `<div>` per la tua istanza del lettore.

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

   Quando viene creato il lettore, all&#39;elemento `<div>` specificato viene assegnata una classe CSS di `ptp-main-video-div-style`. Il DOM risultante sarà simile al seguente:

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. Aggiungi un controllo dell’interfaccia utente.

   Ad esempio, aggiungere una barra di controllo visualizzata quando il mouse passa sopra il lettore:

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

L&#39;oggetto restituito dalla chiamata a `ptp.videoPlayer()` fornisce un comportamento che racchiude l&#39;API del lettore multimediale TVSDK e consente il controllo programmatico della riproduzione. Quando effettui chiamate all&#39;istanza del lettore multimediale, l&#39;interfaccia utente si aggiorna automaticamente in base agli eventi attivati dal lettore multimediale:

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
