---
description: Puoi personalizzare i metadati di inserimento di annunci.
title: Personalizzare i metadati di inserimento di annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Personalizzare i metadati di inserimento di annunci{#customize-ad-insertion-metadata}

Puoi personalizzare i metadati di inserimento di annunci.

1. Imposta un timeout per i metadati pubblicitari per le opportunità non risolte.

   Il valore predefinito per questo timeout è di 20 secondi.
1. Per modificare il valore in 10 secondi, immetti quanto segue:

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   Il `timeout` la proprietà è definita nella `AdvertisingMetadata` e questo timeout può essere impostato per tutte le impostazioni di annunci personalizzati che derivano da `AdvertisingMetadata` classe. Ad esempio, se l’utente definisce delle impostazioni personalizzate per un sistema di risoluzione FreeWheel, può impostare un timeout predefinito utilizzando questa impostazione.

1. Crea `MediaPlayerItemConfig` con le impostazioni dell’annuncio nel passaggio 2.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. Usa questa configurazione durante la chiamata `replaceCurrentResource` il `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```
