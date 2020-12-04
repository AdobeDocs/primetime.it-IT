---
description: Puoi ignorare il comportamento predefinito per il modo in cui TVSDK gestisce le ricerche sugli annunci quando utilizzi indicatori di annunci personalizzati.
seo-description: Puoi ignorare il comportamento predefinito per il modo in cui TVSDK gestisce le ricerche sugli annunci quando utilizzi indicatori di annunci personalizzati.
seo-title: Controllare il comportamento di riproduzione per la ricerca su indicatori di annunci personalizzati
title: Controllare il comportamento di riproduzione per la ricerca su indicatori di annunci personalizzati
uuid: ec95a22f-0143-4c80-826f-d6b40e77cf26
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# Controllare il comportamento di riproduzione per la ricerca di indicatori di annunci personalizzati {#control-playback-behavior-for-seeking-over-custom-ad-markers}

Puoi ignorare il comportamento predefinito per il modo in cui TVSDK gestisce le ricerche sugli annunci quando utilizzi indicatori di annunci personalizzati.

Per impostazione predefinita, quando un utente cerca o passa sezioni di annunci derivanti dal posizionamento di marcatori di annunci personalizzati, TVSDK salta gli annunci. Questo potrebbe essere diverso dal comportamento di riproduzione corrente per le interruzioni pubblicitarie standard. Potete impostare TVSDK per riposizionare l&#39;indicatore di riproduzione all&#39;inizio dell&#39;annuncio personalizzato saltato più di recente quando l&#39;utente cerca oltre uno o più annunci personalizzati.

1. Chiama `CustomRangeMetadata.setAdjustSeekPosition` con `true`.

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
