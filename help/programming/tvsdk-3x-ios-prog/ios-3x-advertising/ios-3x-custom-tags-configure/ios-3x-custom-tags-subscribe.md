---
description: TVSDK prepara oggetti PTTimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel manifesto del contenuto.
title: Iscriviti ai tag personalizzati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 2%

---


# Iscriviti ai tag personalizzati {#subscribe-to-custom-tags}

TVSDK prepara oggetti PTTimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono rilevati nel manifesto del contenuto.

Prima di avviare la riproduzione, è necessario abbonarsi ai tag.
Per ricevere notifiche sui tag personalizzati nei manifesti HLS:

1. Imposta globalmente i nomi dei tag di annunci personalizzati passando una matrice che contiene i tag personalizzati a `setSubscribedTags` in `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >È necessario includere il prefisso `#` quando si lavora con i flussi HLS.

   Ad esempio:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
