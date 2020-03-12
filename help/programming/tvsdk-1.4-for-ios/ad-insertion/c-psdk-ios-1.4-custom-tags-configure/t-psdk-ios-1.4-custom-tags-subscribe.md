---
description: TVSDK prepara oggetti PTTimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.
seo-description: TVSDK prepara oggetti PTTimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.
seo-title: Iscriviti ai tag personalizzati
title: Iscriviti ai tag personalizzati
uuid: de66d3db-46d1-485f-9d3a-6e28495bfb13
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Iscriviti ai tag personalizzati {#subscribe-to-custom-tags}

TVSDK prepara oggetti PTTimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.

Prima di avviare la riproduzione, è necessario effettuare la sottoscrizione ai tag.
Per ricevere notifiche sui tag personalizzati nei manifesti HLS:

1. Imposta i nomi dei tag personalizzati dell&#39;annuncio a livello globale passando un array che contiene i tag personalizzati in `setSubscribedTags` in `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >È necessario includere il `#` prefisso quando si utilizzano i flussi HLS.

   Ad esempio:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```

