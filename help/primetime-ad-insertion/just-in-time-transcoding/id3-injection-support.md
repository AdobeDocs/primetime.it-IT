---
description: La transcodifica just-in-time può inserire metadati ID3 temporizzati nelle creatività degli annunci per facilitare il tracciamento degli annunci lato client.
title: Utilizzo della transcodifica just-in-time per inserire tag di metadati ID3 temporizzati
exl-id: 6171223a-71f9-45a2-a3f5-7ede4a9b101a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---

# Utilizzo della trascodifica just-in-time per inserire tag di metadati temporizzati ID3 {#using-crs-to-inject-id-timed-metadata-tags}

CRS può inserire metadati ID3 temporizzati nelle creatività degli annunci per facilitare il tracciamento degli annunci lato client.

Il lettore client legge i metadati ID3 per abilitare il tracciamento accurato degli annunci.

>[!NOTE]
>
>L’inserimento di metadati a tempo ID3 funziona solo per Safari/iOS.

## Flusso di lavoro per CRS per iniezione ID3 {#workflow-for-crs-for-id3-injection}

Se Primetime Ad Insertion riceve `ptplayer=ios-mobileweb` inserirà i pacchetti ID3 nella creatività dell’annuncio transcodificato prima di caricarli nella rete CDN appropriata per l’archiviazione degli annunci.
