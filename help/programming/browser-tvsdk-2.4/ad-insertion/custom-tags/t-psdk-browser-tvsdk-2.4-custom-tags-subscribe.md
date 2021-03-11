---
description: Il browser TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel file MPD (Media Presentation Description).
title: Iscriviti ai tag personalizzati degli annunci
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 0%

---


# Iscriviti ai tag di annunci personalizzati{#subscribe-to-custom-ad-tags}

Il browser TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel file MPD (Media Presentation Description).

È necessario abbonarsi ai tag prima dell&#39;avvio della riproduzione.
Per abbonarti ai tag, imposta un vettore contenente i nomi dei tag personalizzati sulla proprietà `subscribedTags` . Se devi anche modificare i tag degli annunci utilizzati dal generatore di opportunità predefinito, imposta un vettore che contiene i nomi dei tag degli annunci personalizzati sulla proprietà `adTags` .

Per abbonarti a tag personalizzati:

1. Crea una nuova configurazione di elemento del lettore multimediale.

   ```js
   var mediaPlayerItemConfig = new AdobePSDK.MediPlayerItemConfig();
   ```

1. Crea un vettore stringa vuoto.

   ```js
   var subscribeTags = [];
   ```

1. Aggiungi i nomi dei tag personalizzati a questo vettore.

   >[!IMPORTANT]
   >
   >Se hai a che fare con flussi HLS, ricorda di includere il prefisso `#`.

   ```js
   subscribeTags.push("urn:mpeg:dash:event:2012"); 
   subscribeTags.push("urn:com:adobe:dpi:simple:2015"); 
   ```

1. Assegna il vettore aggiornato alla proprietà `mediaPlayerItemConfig.subscribeTags` .

   ```js
   mediaPlayerItemConfig.subscribeTags = subscribeTags;
   ```

1. Crea un vettore stringa vuoto.

   ```js
   var adTags= [];
   ```

1. Aggiungi il nome del tag di annuncio personalizzato a questo vettore.

   ```js
   adTags.push("urn:com:adobe:dpi:simple:2015");
   ```

1. Assegna il vettore aggiornato alla proprietà `mediaPlayerItemConfig.adTags` .

   ```js
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Utilizza la configurazione dell&#39;elemento del lettore multimediale durante il caricamento del flusso multimediale.

   ```js
   player.replaceCurrentResource(mediaResource,mediaPlayerItemConfig);
   ```

