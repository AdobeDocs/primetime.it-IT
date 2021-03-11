---
description: La transcodifica just-in-time può inserire i metadati timed ID3 nelle creatività degli annunci per facilitare il tracciamento degli annunci lato client.
title: Utilizzo della transcodifica just-in-time per inserire tag di metadati temporizzati ID3
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 0%

---


# Utilizzo della transcodifica just-in-time per inserire tag dei metadati temporizzati ID3 {#using-crs-to-inject-id-timed-metadata-tags}

CRS può inserire i metadati temporizzati ID3 nelle creatività degli annunci per facilitare il tracciamento degli annunci lato client.

Il lettore client legge i metadati ID3 per consentire il tracciamento degli annunci accurato in base al frame.

>[!NOTE]
>
>Funzioni di inserimento dei metadati temporizzati ID3 solo per Safari/iOS.

## Flusso di lavoro per CRS per l&#39;iniezione ID3 {#workflow-for-crs-for-id3-injection}

Se Primetime Ad Insertion riceve il parametro `ptplayer=ios-mobileweb` , inserirà i pacchetti ID3 nella creatività dell&#39;annuncio transcodificato prima di caricarli nel CDN di archiviazione dell&#39;annuncio appropriato.
