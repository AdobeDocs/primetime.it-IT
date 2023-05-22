---
description: Potete controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attiva, viene visualizzato il brano attualmente selezionato. Se modificate la traccia corrente, l'impostazione di visibilità rimane invariata.
title: Controlla la visibilità dei sottotitoli
exl-id: fac24d97-b83e-4bc4-a824-8a1692509519
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---

# Controlla la visibilità dei sottotitoli{#control-closed-caption-visibility}

Potete controllare la visibilità dei sottotitoli codificati. Quando la visibilità è attiva, viene visualizzato il brano attualmente selezionato. Se modificate la traccia corrente, l&#39;impostazione di visibilità rimane invariata.

>[!TIP]
>
>Se il testo con sottotitoli codificati viene visualizzato quando il lettore entra nella modalità di ricerca, non viene più visualizzato dopo il completamento della ricerca. Invece, dopo alcuni secondi, TVSDK mostra il testo della didascalia successiva nel video dopo la posizione di ricerca finale.

>[!NOTE]
>
>I valori di visibilità per i sottotitoli codificati sono definiti in `ClosedCaptionsVisibility`.
>
>
```
>public static const HIDDEN:String = hidden; 
>public static const VISIBLE:String = visible;
>```

1. Attendi `MediaPlayer` avere almeno lo stato PREPARATO (vedere [Attesa di uno stato valido](../../t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)).
1. Per ottenere l&#39;impostazione di visibilità corrente per i sottotitoli, utilizzare il metodo getter in `MediaPlayer`, che restituisce un valore di visibilità.

   ```
   public function get ccVisibility():String
   ```

1. Per modificare la visibilità dei sottotitoli codificati, utilizzate il metodo setter, trasmettendo un valore di visibilità da `ClosedCaptionsVisibility`.

   Ad esempio:

   ```
   public function set ccVisibility(value:String):void
   ```

1. Definisci un elenco a discesa.

   ```
   <s:DropDownList id="ccTracksList" width="85" 
                   dataProvider="{_ccTracks}" 
                   change="onCCTrackChange(event)" 
                   prompt="CC"/>
   ```

1. Definite un array associabile di tracce di sottotitoli.

   ```
   [Bindable] private var _ccTracks:ArrayCollection =  
     new ArrayCollection(); // active tracks 
   ```

1. Configurare i listener.

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
