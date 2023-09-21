---
description: Quando si utilizzano marcatori di annunci personalizzati, è possibile ignorare il comportamento predefinito per la gestione delle ricerche tramite TVSDK sugli annunci.
title: Controlla il comportamento di riproduzione per la ricerca sui marcatori di annunci personalizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Controlla il comportamento di riproduzione per la ricerca sui marcatori di annunci personalizzati {#control-playback-behavior-for-seeking-over-custom-ad-markers}

Quando si utilizzano marcatori di annunci personalizzati, è possibile ignorare il comportamento predefinito per la gestione delle ricerche tramite TVSDK sugli annunci.

Per impostazione predefinita, quando un utente cerca in o nelle sezioni di annunci precedenti che derivano dal posizionamento di marcatori di annunci personalizzati, TVSDK salta gli annunci. Questo comportamento potrebbe differire da quello corrente per le interruzioni pubblicitarie standard. Puoi impostare TVSDK per riposizionare l’indicatore di riproduzione all’inizio dell’annuncio personalizzato saltato più di recente quando l’utente cerca oltre uno o più annunci personalizzati.

1. Chiamata `CustomRangeMetadata.setAdjustSeekPosition` con `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. Utilizzare `customRangeMetadata` in `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```
