---
description: I CRS possono inserire i metadati ID3 temporizzati in formato HLS e creare elementi creativi per facilitare il tracciamento degli annunci lato client.
seo-description: I CRS possono inserire i metadati ID3 temporizzati in formato HLS e creare elementi creativi per facilitare il tracciamento degli annunci lato client.
seo-title: Utilizzo di CRS per inserire tag di metadati temporizzati ID3
title: Utilizzo di CRS per inserire tag di metadati temporizzati ID3
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: c2216a5089d23ca1fcbb77c87b4a01a6fa1807ff
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Utilizzo di CRS per inserire tag di metadati temporizzati ID3 {#using-crs-to-inject-id-timed-metadata-tags}

I CRS possono inserire i metadati ID3 temporizzati in formato HLS e creare elementi creativi per facilitare il tracciamento degli annunci lato client.

Il lettore client legge i metadati ID3 per abilitare il tracciamento degli annunci accurato in base al frame.

>[!NOTE]
>
>L’inserimento di metadati temporizzati ID3 funziona solo su Safari su iOS.

## Flusso di lavoro per CRS per l&#39;iniezione ID3 {#workflow-for-crs-for-id3-injection}

Il flusso di lavoro per l&#39;iniezione ID3 è lo stesso di [Flussi di lavoro dettagliati per il reimballaggio JIT.](../creative-repackaging-service/jit-repackage.md) Se il server di manifesto riceve il  `ptplayer=ios-mobileweb` parametro, dice ai CRS di inserire i pacchetti ID3 nel codice pubblicitario transcodificato prima di caricarlo nel server CDN.

>[!NOTE]
>
>In una configurazione multi-CDN, il server manifesto utilizza il parametro `ptcdn` nell’URL di avvio per identificare il server CDN per caricare l’annuncio creativo.