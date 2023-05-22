---
description: TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel manifesto del contenuto.
title: Iscriviti a tag personalizzati
exl-id: 7a3021cc-d2ba-4a70-9c1f-59766b848a62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# Iscriviti a tag personalizzati{#subscribe-to-custom-tags}

TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel manifesto del contenuto.

Prima di avviare la riproduzione, è necessario iscriversi ai tag.
Per iscriverti ai tag, assegna al vettore un vettore contenente i nomi di tag personalizzati `subscribedTags` proprietà. Se devi modificare anche i tag pubblicitari utilizzati dal generatore di opportunità predefinito, assegna un vettore che contiene i nomi dei tag pubblicitari personalizzati a `adTags` proprietà.

Per ricevere notifiche sui tag personalizzati nei manifesti HLS:

1. Imposta i nomi dei tag personalizzati dell’annuncio a livello globale assegnando a un vettore che contiene i tag personalizzati `subscribeTags` in `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >Devi includere `#` prefisso quando si lavora con flussi HLS.

   Ad esempio:

   ```
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   PSDKConfig.subscribedTags = subscribedTags;
   ```

1. Per modificare globalmente i tag pubblicitari utilizzati dal generatore di opportunità predefinito, assegna un vettore contenente i nomi dei tag pubblicitari personalizzati a `adTags` proprietà in `PSDKConfig`.

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   PSDKConfig.adTags = adTags; 
   ```

1. Per rendere effettive tutte le impostazioni globali, sostituisci la risorsa corrente.

   ```
   player.replaceCurrentResource(mediaResource);
   ```

1. Per impostare i nomi dei tag sottoscritti per un flusso, se necessario:
   1. Crea una configurazione di elemento del lettore multimediale.

      >[!TIP]
      >
      >Il modo più semplice è creare una configurazione predefinita dell’elemento del lettore multimediale.

   1. Assegna un vettore contenente i tag personalizzati a `subscribeTags` in `MediaPlayerItemConfig`.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     new DefaultMediaPlayerItemConfig(); 
   
   var subscribedTags:Vector.<String> = new Vector.<String>(); 
   subscribedTags.push("#EXT-X-ASSET"); 
   subscribedTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.subscribeTags = subscribedTags;
   ```

1. Per modificare i tag di annunci utilizzati dal generatore di opportunità predefinito nel flusso specificato, assegna un vettore contenente i nomi dei tag di annunci personalizzati a `adTags` proprietà in `mediaPlayerItemConfig`

   ```
   var adTags:Vector.<String> = new Vector.<String>(); 
   adTags.push("#EXT-X-AD"); 
   mediaPlayerItemConfig.adTags = adTags;
   ```

1. Per rendere effettive le modifiche per il flusso, durante il caricamento del flusso multimediale utilizza la configurazione dell’elemento del lettore multimediale.

   ```
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
