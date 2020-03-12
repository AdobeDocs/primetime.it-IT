---
description: TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.
seo-description: TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.
seo-title: Iscriviti ai tag personalizzati
title: Iscriviti ai tag personalizzati
uuid: 9f74b2b9-bbc9-433c-8226-2c2b68eddf7e
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Iscriviti ai tag personalizzati {#subscribe-to-custom-tags}

TVSDK prepara gli oggetti TimedMetadata per i tag sottoscritti ogni volta che questi oggetti vengono incontrati nel manifesto del contenuto.

Prima di avviare la riproduzione, è necessario effettuare la sottoscrizione ai tag. Per ricevere notifiche sui tag personalizzati nei manifesti HLS:

1. Imposta i nomi dei tag personalizzati dell&#39;annuncio a livello globale passando un array che contiene i tag personalizzati in `setSubscribedTags` in `MediaPlayerItemConfig`.

   >[!IMPORTANT]
   >
   >È necessario includere il `#` prefisso quando si utilizzano i flussi HLS.

   Ad esempio:

   ```java
   String[] array = new String[3]; 
   array[0] = "#EXT-X-ASSET"; 
   array[1] = "#EXT-X-BLACKOUT"; 
   array[2] = "#EXT-OATCLS-SCTE35"; 
   MediaPlayerItemConfig.setSubscribedTags(array);
   ```

