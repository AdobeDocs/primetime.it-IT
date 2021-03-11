---
description: È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attiva, viene visualizzata la traccia attualmente selezionata. Se modifichi la traccia corrente, l’impostazione di visibilità rimane la stessa.
title: Controllo della visibilità dei sottotitoli
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# Controllare la visibilità dei sottotitoli{#control-closed-caption-visibility}

È possibile controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attiva, viene visualizzata la traccia attualmente selezionata. Se modifichi la traccia corrente, l’impostazione di visibilità rimane la stessa.

>[!TIP]
>
>Se il testo della didascalia chiusa viene visualizzato quando il lettore entra nella modalità di ricerca, il testo non viene più visualizzato al termine della ricerca. Al contrario, dopo alcuni secondi, TVSDK visualizza il testo della didascalia successiva nel video dopo la posizione di ricerca finale.

>[!NOTE]
>
>I valori di visibilità dei sottotitoli codificati sono definiti in `ClosedCaptionsVisibility`.
>
>
```
>public static const HIDDEN:String = hidden; 
>public static const VISIBLE:String = visible;
>```

1. Attendere che il `MediaPlayer` disponga almeno dello stato PREPARATO (vedere [Attendere che uno stato valido](../../t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)).
1. Per ottenere l’impostazione di visibilità corrente per i sottotitoli codificati, utilizza il metodo getter in `MediaPlayer`, che restituisce un valore di visibilità.

   ```
   public function get ccVisibility():String
   ```

1. Per modificare la visibilità dei sottotitoli codificati, utilizzare il metodo setter, passando un valore di visibilità da `ClosedCaptionsVisibility`.

   Ad esempio:

   ```
   public function set ccVisibility(value:String):void
   ```

1. Definire un elenco a discesa.

   ```
   <s:DropDownList id="ccTracksList" width="85" 
                   dataProvider="{_ccTracks}" 
                   change="onCCTrackChange(event)" 
                   prompt="CC"/>
   ```

1. Definire una matrice associabile di tracce di didascalia chiusa.

   ```
   [Bindable] private var _ccTracks:ArrayCollection =  
     new ArrayCollection(); // active tracks 
   ```

1. Imposta ascoltatori.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

   Per rimuovere i listener dal codice di distruzione:

   ```
   player.removeEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.removeEventListener(MediaPlayerItemEvent.CAPTIONS_UPDATED, onCaptionUpdated);
   ```

1. Crea e aggiorna l’elenco quando un utente effettua una scelta dall’elenco.

   ```
   private function onCCTrackChange(event:IndexChangeEvent):void { 
       var ccTrackIndex:int = event.newIndex; 
       var ccTracks:Vector.<ClosedCaptionsTrack> =  
         _player.currentItem.closedCaptionsTracks; 
       if (ccTrackIndex == 0) { 
           _player.ccVisibility = MediaPlayer.INVISIBLE; 
       } 
       else if (ccTrackIndex <= _ccTracks.length) { 
           var index:Number = findFromActiveIndex(ccTracks, ccTrackIndex - 1); 
           _player.currentItem.selectClosedCaptionsTrack(ccTracks[index]); 
           _player.ccVisibility = MediaPlayer.VISIBLE; 
       } 
   } 
   
   private function findFromActiveIndex(ccTracks:Vector.<ClosedCaptionsTrack>,  
     ccTrackIndex:int):Number { 
       var count:Number = 0; 
       for each (var ccTrack:ClosedCaptionsTrack in ccTracks) { 
           if (count < ccTrackIndex) 
               count = count + 1; 
           else 
               return count; 
       } 
       return -1; 
   } 
   
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       ... (you are likely to need more code here for other reasons) 
       updateCCTracks(_player.currentItem.closedCaptionsTracks); 
   } 
   
   private function onCaptionUpdated(event:MediaPlayerItemEvent):void { 
       ... (you are likely to need more code here for other reasons) 
       updateCCTracks(_player.currentItem.closedCaptionsTracks,  
                     (_player.ccVisibility == MediaPlayer.VISIBLE) ?  
                      _player.currentItem.selectedClosedCaptionsTrack : null); 
   } 
   
   private function updateCCTracks(tracks:Vector.<ClosedCaptionsTrack>,  
     selectedTrack:ClosedCaptionsTrack = null):void { 
       _ccTracks.removeAll(); 
   
       _ccTracks.addItem( 
           { 
               "label": "CC off", 
               "data": "cc-off" 
           } 
       ); 
   
       var selectedIndex:int = 0; 
       for each (var ccTrack:ClosedCaptionsTrack in tracks) { 
           _ccTracks.addItem( 
               { 
                   "label": ccTrack.name, 
                   "data": ccTrack.name 
               } 
           ); 
           if (selectedTrack && ccTrack.name == selectedTrack.name && 
           ccTrack.language == selectedTrack.language && 
           ccTrack.serviceType == selectedTrack.serviceType) { 
               selectedIndex = _ccTracks.length - 1; 
           } 
       } 
   
       var hasCC:Boolean = _ccTracks.length > 0; 
       ccTracksList.enabled = hasCC; 
       ccTracksList.mouseEnabled = hasCC; 
       ccTracksList.selectedIndex = selectedIndex; 
   } 
   ```

