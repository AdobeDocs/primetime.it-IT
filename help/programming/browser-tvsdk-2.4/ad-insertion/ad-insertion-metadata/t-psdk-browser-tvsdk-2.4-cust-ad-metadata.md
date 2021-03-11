---
description: Puoi personalizzare i metadati dell’inserimento di annunci.
title: Personalizzare i metadati di inserimento degli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---


# Personalizza metadati di inserimento annunci{#customize-ad-insertion-metadata}

Puoi personalizzare i metadati dell’inserimento di annunci.

1. Imposta un timeout sui metadati pubblicitari per le opportunità non risolte.

   Il valore predefinito per questo timeout è 20 secondi.
1. Per modificare il valore in 10 secondi, immetti quanto segue:

   ```js
   auditudeSettings.timeout = 10000; //this value is specified in milliseconds
   ```

   La proprietà `timeout` è definita nella classe `AdvertisingMetadata` e questo timeout può essere impostato per tutte le impostazioni di annunci personalizzate derivanti dalla classe `AdvertisingMetadata` . Ad esempio, se gli utenti definiscono impostazioni personalizzate per un risolutore FreeWheel, possono impostare un timeout predefinito utilizzando questa impostazione.

1. Crea `MediaPlayerItemConfig` con le impostazioni dell&#39;annuncio nel passaggio 2.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings;
   ```

1. Utilizza questa configurazione per chiamare `replaceCurrentResource` su `MediaPlayer`.

   ```js
   player.replaceCurrentResource(mediaResource, config);
   ```

