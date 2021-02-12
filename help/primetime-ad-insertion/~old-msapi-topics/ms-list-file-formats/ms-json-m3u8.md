---
description: Se pttrackingmode=simple o ptplayer=ios-mobileweb, il server di manifesto invia nuovamente un file in formato JSON contenente Master-M3U8, un URL che il client deve utilizzare per richiedere il file M3U8 che descrive il contenuto.
seo-description: Se pttrackingmode=simple o ptplayer=ios-mobileweb, il server di manifesto invia nuovamente un file in formato JSON contenente Master-M3U8, un URL che il client deve utilizzare per richiedere il file M3U8 che descrive il contenuto.
seo-title: Formato JSON per l'URL per la richiesta di playlist con manifesto variante
title: Formato JSON per l'URL per la richiesta di playlist con manifesto variante
uuid: 9f9693d0-3c93-4555-b20c-7f4576742f41
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Formato JSON per l&#39;URL per la richiesta della playlist del manifesto variante {#json-format-for-url-for-requesting-variant-manifest-playlist}

Se `pttrackingmode=simple` o `ptplayer=ios-mobileweb`, il server manifesto invia un file in formato JSON contenente Master-M3U8, un URL che il client deve utilizzare per richiedere il file M3U8 che descrive il contenuto.

Questo è il formato del file JSON contenente l&#39;URL `Master-M3U8`.

```
{
"Master-M3U8": "https://manifest.auditude.com/auditude/variant/{publisherAssetID}/
  {sessionId}/{Base 64 of the url of the content}.m3u8
  ?u={Ad Request Id}
  &z={Ad Zone Id}
  &pttrackingmode=simple
  &pttrackingversion=v1
  &{other query parameters}"
}
```
