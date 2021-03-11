---
description: TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel manifesto del contenuto.
title: Iscriviti ai tag personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---


# Iscriviti ai tag personalizzati{#subscribe-to-custom-tags}

TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel manifesto del contenuto.

Prima di avviare la riproduzione, è necessario abbonarsi ai tag.
Per abbonarti ai tag, assegna un vettore contenente i nomi dei tag personalizzati alla proprietà `subscribedTags` . Se devi anche modificare i tag dell&#39;annuncio utilizzati dal generatore di opportunità predefinito, assegna alla proprietà `adTags` un vettore contenente i nomi dei tag dell&#39;annuncio personalizzato.

Per ricevere notifiche sui tag personalizzati nei manifesti HLS:

1. Imposta i nomi dei tag di annunci personalizzati a livello globale assegnando un vettore che contiene i tag personalizzati a `subscribeTags` in `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >È necessario includere il prefisso `#` quando si lavora con i flussi HLS.

   Ad esempio:

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. Per modificare globalmente i tag degli annunci utilizzati dal generatore di opportunità predefinito, assegna un vettore che contiene i nomi dei tag degli annunci personalizzati alla proprietà `adTags` in `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. Affinché tutte le impostazioni globali abbiano effetto, sostituisci la risorsa corrente.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. Per impostare i nomi dei tag sottoscritti per un flusso, se necessario:
   1. Crea una configurazione di un elemento del lettore multimediale.

      >[!TIP]
      >
      >Il modo più semplice è quello di creare una configurazione predefinita degli elementi del lettore multimediale.

   1. Assegna un vettore contenente i tag personalizzati a `subscribeTags` in `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. Per modificare i tag degli annunci utilizzati dal generatore di opportunità predefinito nel flusso specificato, assegna un vettore che contiene i nomi dei tag degli annunci personalizzati alla proprietà `adTags` in `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Affinché le modifiche per il flusso abbiano effetto, durante il caricamento del flusso multimediale, utilizza la configurazione dell&#39;elemento del lettore multimediale.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

