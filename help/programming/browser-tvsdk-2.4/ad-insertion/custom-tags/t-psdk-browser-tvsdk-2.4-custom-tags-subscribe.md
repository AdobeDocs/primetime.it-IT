---
description: Il browser TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel file MPD (Media Presentation Description).
title: Iscriviti ai tag annuncio personalizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---

# Iscriviti ai tag annuncio personalizzati{#subscribe-to-custom-ad-tags}

Il browser TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel file MPD (Media Presentation Description).

È necessario sottoscrivere i tag prima di avviare la riproduzione.
Per abbonarti ai tag, imposta un vettore contenente i nomi dei tag personalizzati su `subscribedTags` proprietà. Se inoltre devi modificare i tag annuncio utilizzati dal generatore di opportunità predefinito, imposta un vettore contenente i nomi dei tag annuncio personalizzati su `adTags` proprietà.

Per abbonarsi a tag personalizzati:

1. Crea una nuova configurazione di elemento del lettore multimediale.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. Crea un vettore di stringa vuoto.

   ```js
   var subscribeTags = [];
   ```

1. Aggiungi i nomi di tag personalizzati a questo vettore.

   >[!IMPORTANT]
   >
   >Se stai trattando con flussi HLS, ricorda di includere `#` prefisso.

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. Assegna il vettore aggiornato a `mediaPlayerItemConfig.subscribeTags` proprietà.

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. Crea un vettore di stringa vuoto.

   ```js
   var adTags= [];
   ```

1. Aggiungi il nome del tag annuncio personalizzato a questo vettore.

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. Assegna il vettore aggiornato a `mediaPlayerItemConfig.adTags` proprietà.

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Utilizza la configurazione dell’elemento del lettore multimediale durante il caricamento del flusso multimediale.

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```
