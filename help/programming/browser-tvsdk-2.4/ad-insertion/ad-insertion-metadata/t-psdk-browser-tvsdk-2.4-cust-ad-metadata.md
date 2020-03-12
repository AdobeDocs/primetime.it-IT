---
description: Potete personalizzare i metadati di inserimento e inserimento.
seo-description: Potete personalizzare i metadati di inserimento e inserimento.
seo-title: Personalizzare i metadati di inserimento annunci
title: Personalizzare i metadati di inserimento annunci
uuid: 047470d3-45bd-48be-82ce-4e9d9fe6ea10
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Personalizzare i metadati di inserimento annunci{#customize-ad-insertion-metadata}

Potete personalizzare i metadati di inserimento e inserimento.

1. Impostate un timeout sui metadati della pubblicità per le opportunità non risolte.

   Il valore predefinito per questo timeout è 20 secondi.
1. Per modificare il valore in 10 secondi, immettete quanto segue:

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   La `timeout` proprietà è definita nella `AdvertisingMetadata` classe e questo timeout può essere impostato per qualsiasi impostazione di annuncio personalizzata derivata dalla `AdvertisingMetadata` classe. Ad esempio, se gli utenti definiscono impostazioni personalizzate per un risolutore FreeWheel, possono impostare un timeout predefinito utilizzando questa impostazione.

1. Crea `MediaPlayerItemConfig` con le impostazioni degli annunci nel passaggio 2.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. Utilizzate questa configurazione quando effettuate una chiamata `replaceCurrentResource` a `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

