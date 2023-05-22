---
description: Le richieste dei client per l’inserimento di annunci specificano in genere più di una velocità in bit nella variante della playlist in formato M3U8. Il server manifesto genera e restituisce un nuovo file M3U8 variante contenente un collegamento M3U8 separato per ogni velocità bit. Genera anche un ID gruppo univoco per collegare questi M3U8s.
title: Più flussi di bit rate
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Più flussi di bit rate {#multiple-bit-rate-streams}

Le richieste dei client per l’inserimento di annunci specificano in genere più di una velocità in bit nella variante della playlist in formato M3U8. Il server manifesto genera e restituisce un nuovo file M3U8 variante contenente un collegamento M3U8 separato per ogni velocità bit. Genera anche un ID gruppo univoco per collegare questi M3U8s.

Il server manifest utilizza le informazioni contenute nella richiesta Bootstrap URL del client per recuperare la playlist delle varianti di contenuto. Genera una nuova playlist di varianti contenente i collegamenti del server manifesto al contenuto a livello di flusso. Il client le utilizza per creare richieste di inserimento di annunci. I collegamenti di contenuto a livello di flusso del server manifesto hanno il seguente formato:

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** Il server manifesto imposta questo valore in base al tipo di playlist del contenuto: Live/linear (#EXT-X-PLAYLIST-TYPE:EVENT) o VOD (#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** ID univoco dell’editore per il contenuto specifico fornito nella richiesta URL Bootstrap.

* **`rendition`** Il server manifesto imposta questo valore in base al valore BANDWIDTH del flusso di contenuto e lo utilizza per far corrispondere la velocità in bit dell’annuncio alla velocità in bit del contenuto. La velocità in bit dell’annuncio non può superare la velocità in bit del contenuto, a meno che non lo faccia la rappresentazione dell’annuncio con la velocità in bit più bassa.

* **`groupID`** Il server manifest genera questo valore e lo utilizza per garantire che inserisca gli annunci in modo coerente, indipendentemente dalla velocità di trasmissione dei rendering richiesta dal client.

* **`base64-encoded url of the bit rate stream`** Il server manifesto URL-safe base64 codifica l&#39;URL assoluto del flusso di contenuto. Ogni flusso ha il proprio URL.

* **`Query parameters`** Parametri di query forniti nella richiesta URL Bootstrap.

