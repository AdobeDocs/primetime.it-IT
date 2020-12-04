---
description: Potete ignorare il comportamento predefinito per il modo in cui TVSDK cerca sugli annunci quando si utilizzano gli indicatori di annunci personalizzati.
seo-description: Potete ignorare il comportamento predefinito per il modo in cui TVSDK cerca sugli annunci quando si utilizzano gli indicatori di annunci personalizzati.
seo-title: Controllare il comportamento di riproduzione per la ricerca su indicatori di annunci personalizzati
title: Controllare il comportamento di riproduzione per la ricerca su indicatori di annunci personalizzati
uuid: cf973caf-be29-46ce-bfa4-651e7653f8d4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Controllare il comportamento di riproduzione per la ricerca su indicatori di annunci personalizzati{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Potete ignorare il comportamento predefinito per il modo in cui TVSDK cerca sugli annunci quando si utilizzano gli indicatori di annunci personalizzati.

Per impostazione predefinita, quando un utente cerca o passa sezioni di annunci derivanti dal posizionamento di marcatori di annunci personalizzati, TVSDK salta gli annunci. Questo potrebbe essere diverso dal comportamento di riproduzione corrente per le interruzioni pubblicitarie standard.

Potete indicare a TVSDK di riposizionare l&#39;indicatore di riproduzione all&#39;inizio dell&#39;annuncio personalizzato saltato più di recente quando l&#39;utente cerca oltre uno o più annunci personalizzati.

1. Configurate un&#39;istanza di metadati con l&#39;enumerazione `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` impostata sul valore stringa &quot;true&quot; (non come booleano `true`).

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. Create e configurate un&#39;istanza `MediaResource`, passando le opzioni di configurazione aggiuntive a `TimeRangeCollection.toMetadata`. Questo metodo riceve opzioni di configurazione aggiuntive tramite un’altra struttura di metadati generica.

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```

