---
description: Se pttrackingmode=simple o ptplayer=ios-mobileweb, il server manifest invia un file in formato JSON contenente Master-M3U8, un URL da utilizzare per richiedere il file M3U8 che descrive il contenuto.
title: Formato JSON per l’URL per la richiesta della playlist del manifesto di variante
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# Formato JSON per l&#39;URL per la richiesta della playlist del manifesto di variante {#json-format-for-url-for-requesting-variant-manifest-playlist}

Se `pttrackingmode=simple` o `ptplayer=ios-mobileweb`, il server manifesto invia un file in formato JSON contenente Master-M3U8, un URL da utilizzare per richiedere il file M3U8 che descrive il contenuto.

Questo è il formato del file JSON contenente l&#39; `Master-M3U8` URL.

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
