---
description: TVSDK prepara oggetti PTTimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.
seo-description: TVSDK prepara oggetti PTTimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.
seo-title: Iscriviti ai tag personalizzati
title: Iscriviti ai tag personalizzati
uuid: e47076b2-6184-4c20-bae4-ba7ae62cf198
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 1%

---


# Iscriviti ai tag personalizzati {#subscribe-to-custom-tags}

TVSDK prepara oggetti PTTimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.

Prima di avviare la riproduzione, è necessario effettuare la sottoscrizione ai tag.
Per ricevere notifiche sui tag personalizzati nei manifesti HLS:

1. Impostate i nomi dei tag degli annunci personalizzati a livello globale passando un array che contiene i tag personalizzati a `setSubscribedTags` in `PTSDKConfig`.

   >[!IMPORTANT]
   >
   >È necessario includere il prefisso `#` quando si utilizzano i flussi HLS.

   Ad esempio:

   ```
   NSArray *customHLSTags = [NSArray arrayWithObjects:@"#EXT-OATCLS-SCTE35",@"#EXT_CUSTOM_TAG2",nil]; 
   [PTSDKConfig  setSubscribedTags:customHLSTags];
   ```
