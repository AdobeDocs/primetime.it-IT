---
description: Le richieste dei clienti per l'inserimento di annunci in genere specificano più bitrate nella sequenza di riproduzione della variante in formato M3U8. Il server di manifesto genera e restituisce una nuova variante del file M3U8 contenente un collegamento M3U8 separato per ogni bitrate. Viene inoltre generato un ID gruppo univoco per collegare questi M3U8s.
seo-description: Le richieste dei clienti per l'inserimento di annunci in genere specificano più bitrate nella sequenza di riproduzione della variante in formato M3U8. Il server di manifesto genera e restituisce una nuova variante del file M3U8 contenente un collegamento M3U8 separato per ogni bitrate. Viene inoltre generato un ID gruppo univoco per collegare questi M3U8s.
seo-title: Flussi bitrate multipli
title: Flussi bitrate multipli
uuid: f59cb765-e000-43e0-8d3a-8149a3c5b96e
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Flussi bitrate multipli {#multiple-bit-rate-streams}

Le richieste dei clienti per l&#39;inserimento di annunci in genere specificano più bitrate nella sequenza di riproduzione della variante in formato M3U8. Il server di manifesto genera e restituisce una nuova variante del file M3U8 contenente un collegamento M3U8 separato per ogni bitrate. Viene inoltre generato un ID gruppo univoco per collegare questi M3U8s.

Il server manifesto utilizza le informazioni contenute nella richiesta dell&#39;URL di Bootstrap del client per recuperare la playlist della variante di contenuto. Viene generata una nuova playlist di variante contenente collegamenti del server manifesto al contenuto a livello di flusso. Il client li utilizza per creare richieste di inserimento di annunci. I collegamenti del contenuto a livello di flusso del server manifesto hanno il formato seguente:

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** Il server manifesto imposta questo valore in base al tipo di playlist del contenuto: Live/linear (#EXT-X-PLAYLIST-TYPE:EVENT) o VOD (#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** ID univoco dell&#39;editore per il contenuto specifico fornito nella richiesta di Bootstrap URL.

* **`rendition`** Il server manifesto imposta questo valore in base al valore BANDWIDTH del flusso di contenuto e lo utilizza per corrispondere al bitrate dell&#39;annuncio al bitrate del contenuto. Il bitrate dell&#39;annuncio non può superare il bitrate del contenuto a meno che la rappresentazione dell&#39;annuncio con il bitrate più basso non lo faccia.

* **`groupID`** Il server del manifesto genera questo valore e lo utilizza per garantire che gli annunci vengano inseriti in modo coerente, indipendentemente dal rendering del bitrate richiesto dal client.

* **`base64-encoded url of the bit rate stream`** Il server manifesto URL-safe base64 codifica l&#39;URL assoluto del flusso di contenuto. Ogni flusso ha un proprio URL.

* **`Query parameters`** Parametri di query forniti nella richiesta dell&#39;URL di Bootstrap.

