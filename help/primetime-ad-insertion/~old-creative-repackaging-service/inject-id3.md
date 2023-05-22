---
description: CRS può inserire metadati temporizzati ID3 nel formato HLS e nelle creatività per facilitare il tracciamento degli annunci lato client.
title: Utilizzo di CRS per inserire tag di metadati temporizzati ID3
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Utilizzo di CRS per inserire tag di metadati temporizzati ID3 {#using-crs-to-inject-id-timed-metadata-tags}

CRS può inserire metadati temporizzati ID3 nel formato HLS e nelle creatività per facilitare il tracciamento degli annunci lato client.

Il lettore client legge i metadati ID3 per abilitare il tracciamento accurato degli annunci.

>[!NOTE]
>
>L’inserimento di metadati a tempo ID3 funziona solo su Safari su iOS.

## Flusso di lavoro per CRS per iniezione ID3 {#workflow-for-crs-for-id3-injection}

Il flusso di lavoro per l’iniezione di ID3 è lo stesso della [Flussi di lavoro dettagliati per il riconfezionamento JIT.](../~old-creative-repackaging-service/jit-repackage.md) Se il server manifesto riceve `ptplayer=ios-mobileweb` indica a CRS di inserire pacchetti ID3 nella creatività dell’annuncio transcodificato prima di caricarli sul server CDN.

>[!NOTE]
>
>In una configurazione con più reti CDN, il server manifest utilizza `ptcdn` parametro nell’URL di avvio per identificare il server CDN su cui caricare la creatività dell’annuncio.