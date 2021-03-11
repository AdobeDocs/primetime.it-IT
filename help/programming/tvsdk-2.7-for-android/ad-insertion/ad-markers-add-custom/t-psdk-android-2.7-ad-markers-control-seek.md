---
description: È possibile ignorare il comportamento predefinito per il modo in cui TVSDK gestisce le ricerche sugli annunci quando si utilizzano gli ad markers personalizzati.
title: Controllare il comportamento di riproduzione per la ricerca di indicatori di annunci personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Controllare il comportamento di riproduzione per la ricerca di marcatori di annunci personalizzati {#control-playback-behavior-for-seeking-over-custom-ad-markers}

È possibile ignorare il comportamento predefinito per il modo in cui TVSDK gestisce le ricerche sugli annunci quando si utilizzano gli ad markers personalizzati.

Per impostazione predefinita, quando un utente cerca nelle sezioni o nelle sezioni precedenti degli annunci risultanti dal posizionamento di marcatori pubblicitari personalizzati, TVSDK salta gli annunci. Questo potrebbe differire dal comportamento di riproduzione corrente per le interruzioni pubblicitarie standard. Puoi impostare TVSDK per riposizionare l’indicatore di riproduzione all’inizio dell’annuncio personalizzato saltato più di recente quando l’utente cerca oltre uno o più annunci personalizzati.

1. Chiama `CustomRangeMetadata.setAdjustSeekPosition` con `true`.

   ```java
   customRangeMetadata.setAdjustSeekPosition (true);
   ```

1. Utilizza `customRangeMetadata` in `MediaPlayerItemConfig`.

   ```java
   // Set customRangeMetadata 
   config.setCustomRangeMetadata(customRangeMetadata); 
   
   // prepare the content for playback by calling replaceCurrentResource 
   mediaPlayer.replaceCurrentResource(mediaResource, config); 
   ```

