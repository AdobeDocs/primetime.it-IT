---
description: TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.
seo-description: TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.
seo-title: Iscriviti ai tag personalizzati
title: Iscriviti ai tag personalizzati
uuid: 43480265-4951-466a-a347-6debfb6935ee
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Iscriviti a tag personalizzati{#subscribe-to-custom-tags}

TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.

Prima di avviare la riproduzione, è necessario effettuare la sottoscrizione ai tag.
Per sottoscrivere un&#39;iscrizione ai tag, assegnate un vettore contenente i nomi dei tag personalizzati alla proprietà `subscribedTags`. Per modificare anche i tag degli annunci utilizzati dal generatore di opportunità predefinito, assegnate un vettore che contiene i nomi dei tag degli annunci personalizzati alla proprietà `adTags`.

Per ricevere notifiche sui tag personalizzati nei manifesti HLS:

1. Impostate i nomi dei tag di annunci personalizzati a livello globale assegnando un vettore che contiene i tag personalizzati a `subscribeTags` in `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >È necessario includere il prefisso `#` quando si utilizzano i flussi HLS.

   Ad esempio:

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. Per modificare globalmente i tag degli annunci utilizzati dal generatore di opportunità predefinito, assegnate un vettore che contiene i nomi dei tag degli annunci personalizzati alla proprietà `adTags` in `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. Per rendere attive tutte le impostazioni globali, sostituire la risorsa corrente.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. Per impostare i nomi dei tag sottoscritti per un flusso, se necessario:
   1. Creare una configurazione di elemento del lettore multimediale.

      >[!TIP]
      >
      >Il modo più semplice è quello di creare una configurazione di elemento del lettore multimediale predefinita.

   1. Assegnare un vettore contenente i tag personalizzati a `subscribeTags` in `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. Per modificare i tag degli annunci utilizzati dal generatore di opportunità predefinito nel flusso specificato, assegnate un vettore che contiene i nomi dei tag degli annunci personalizzati alla proprietà `adTags` in `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Affinché le modifiche apportate al flusso diventino effettive, al momento del caricamento del flusso multimediale utilizzate la configurazione dell&#39;elemento del lettore multimediale.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

