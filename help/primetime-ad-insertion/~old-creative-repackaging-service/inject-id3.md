---
description: CRS può inserire i metadati temporizzati ID3 nel formato HLS e creare contenuti per facilitare il tracciamento degli annunci lato client.
title: Utilizzo di CRS per inserire tag dei metadati temporizzati ID3
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Utilizzo di CRS per inserire tag dei metadati temporizzati ID3 {#using-crs-to-inject-id-timed-metadata-tags}

CRS può inserire i metadati temporizzati ID3 nel formato HLS e creare contenuti per facilitare il tracciamento degli annunci lato client.

Il lettore client legge i metadati ID3 per consentire il tracciamento degli annunci accurato in base al frame.

>[!NOTE]
>
>L’iniezione di metadati temporizzati ID3 funziona solo su Safari su iOS.

## Flusso di lavoro per CRS per l&#39;iniezione ID3 {#workflow-for-crs-for-id3-injection}

Il flusso di lavoro per l’iniezione ID3 è lo stesso di in [Flussi di lavoro dettagliati per il repackaging JIT.](../~old-creative-repackaging-service/jit-repackage.md) Se il server manifest riceve il  `ptplayer=ios-mobileweb` parametro , dice a CRS di inserire i pacchetti ID3 nell&#39;annuncio pubblicitario transcodificato prima di caricarli nel server CDN.

>[!NOTE]
>
>In una configurazione multi-CDN, il server manifesto utilizza il parametro `ptcdn` nell&#39;URL di avvio per identificare il server CDN per caricare la creatività dell&#39;annuncio.