---
description: Quando utilizzi i marcatori di annunci personalizzati, puoi sovrascrivere il comportamento predefinito per la ricerca di TVSDK sugli annunci.
title: Controlla il comportamento di riproduzione per la ricerca sui marcatori di annunci personalizzati
exl-id: 83faa5a4-4416-499e-8cf2-d016cd9a379d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---

# Controlla il comportamento di riproduzione per la ricerca sui marcatori di annunci personalizzati{#control-playback-behavior-for-seeking-over-custom-ad-markers}

Quando utilizzi i marcatori di annunci personalizzati, puoi sovrascrivere il comportamento predefinito per la ricerca di TVSDK sugli annunci.

Per impostazione predefinita, quando un utente cerca in o nelle sezioni di annunci precedenti che derivano dal posizionamento di marcatori di annunci personalizzati, TVSDK salta gli annunci. Questo comportamento potrebbe differire da quello corrente per le interruzioni pubblicitarie standard.

Puoi dire a TVSDK di riposizionare la testina di riproduzione all’inizio dell’annuncio personalizzato saltato più di recente quando l’utente cerca oltre uno o più annunci personalizzati.

1. Configurare un’istanza di metadati con `DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` enumerazione impostata sul valore stringa &quot;true&quot; (non come booleano) `true`).

   ```java
   Metadata metadata = new MetadataNode(); 
   metadata.setValue(DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED.getValue(),"true");
   ```

1. Creare e configurare un `MediaResource` , passando le opzioni di configurazione aggiuntive a `TimeRangeCollection.toMetadata`. Questo metodo riceve opzioni di configurazione aggiuntive tramite un’altra struttura di metadati generica.

   ```java
   MediaResource mediaResource =  
     MediaResource.createFromUrl("www.example.com/video/test_video.m3u8", 
                                 timeRanges.toMetadata(metadata));
   ```
