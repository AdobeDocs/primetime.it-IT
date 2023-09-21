---
description: TVSDK prepara gli oggetti PTTimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel manifesto del contenuto.
title: Iscriviti a tag personalizzati
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Iscriviti a tag personalizzati {#subscribe-to-custom-tags}

TVSDK prepara gli oggetti PTTimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel manifesto del contenuto.

Prima di avviare la riproduzione, è necessario iscriversi ai tag.
Per ricevere notifiche sui tag personalizzati nei manifesti HLS:

1. Imposta i nomi dei tag personalizzati dell’annuncio a livello globale trasmettendo un array che contiene i tag personalizzati a `setSubscribedTags` in `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >Devi includere `#` prefisso quando si lavora con flussi HLS.

   Ad esempio:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
