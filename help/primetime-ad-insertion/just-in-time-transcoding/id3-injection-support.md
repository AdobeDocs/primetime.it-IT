---
description: La transcodifica "just-in-time" può iniettare i metadati ID3 temporizzati nelle creatività degli annunci pubblicitari per facilitare il tracciamento degli annunci lato client.
seo-description: La transcodifica "just-in-time" consente di inserire i metadati ID3 temporizzati nel formato HLS e nelle creatività per facilitare il tracciamento degli annunci lato client.
seo-title: Utilizzo della transcodifica just-in-time per inserire tag di metadati temporizzati ID3
title: Utilizzo della transcodifica just-in-time per inserire tag di metadati temporizzati ID3
uuid: 491bbb9e-15de-4871-baa1-f7bb0ea0dde2
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 0%

---


# Utilizzo della transcodifica Just-in-Time per inserire tag di metadati temporizzati ID3 {#using-crs-to-inject-id-timed-metadata-tags}

Il CRS può inserire i metadati ID3 temporizzati nelle creatività degli annunci per facilitare il tracciamento degli annunci lato client.

Il lettore client legge i metadati ID3 per abilitare il tracciamento degli annunci accurato in base al frame.

>[!NOTE]
>
>Le funzioni di inserimento di metadati temporizzati ID3 sono disponibili solo per Safari/iOS.

## Flusso di lavoro per CRS per l&#39;iniezione ID3 {#workflow-for-crs-for-id3-injection}

Se il Ad Insertion Primetime  riceve il parametro `ptplayer=ios-mobileweb`, immetterà i pacchetti ID3 nel codice pubblicitario transcodificato prima di caricare nel CDN di archiviazione appropriato.
