---
description: Il browser TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel file MPD (Media Presentation Description).
seo-description: Il browser TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel file MPD (Media Presentation Description).
seo-title: Iscriviti ai tag pubblicitari personalizzati
title: Iscriviti ai tag pubblicitari personalizzati
uuid: 208f61f4-dc33-4363-aa71-878458740a8d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Iscriviti a tag pubblicitari personalizzati{#subscribe-to-custom-ad-tags}

Il browser TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel file MPD (Media Presentation Description).

Prima di avviare la riproduzione, dovete abbonarvi ai tag.
Per sottoscrivere un’iscrizione ai tag, impostare un vettore contenente i nomi dei tag personalizzati sulla proprietà `subscribedTags`. Se dovete anche modificare i tag degli annunci utilizzati dal generatore di opportunità predefinito, impostate un vettore che contiene i nomi dei tag degli annunci personalizzati sulla proprietà `adTags`.

Per effettuare la sottoscrizione ai tag personalizzati:

1. Crea una nuova configurazione di elemento del lettore multimediale.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. Create un vettore stringa vuoto.

   ```js
   var subscribeTags = [];
   ```

1. Aggiungete i nomi dei tag personalizzati a questo vettore.

   >[!IMPORTANT]
   >
   >Se avete a che fare con flussi HLS, ricordate di includere il prefisso `#`.

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. Assegnare il vettore aggiornato alla proprietà `mediaPlayerItemConfig.subscribeTags`.

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. Create un vettore stringa vuoto.

   ```js
   var adTags= [];
   ```

1. Aggiungi il nome del tag personalizzato dell&#39;annuncio a questo vettore.

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. Assegnare il vettore aggiornato alla proprietà `mediaPlayerItemConfig.adTags`.

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Utilizzate la configurazione dell&#39;elemento del lettore multimediale quando caricate il flusso multimediale.

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```

