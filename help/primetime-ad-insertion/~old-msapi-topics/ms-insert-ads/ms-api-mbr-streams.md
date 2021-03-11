---
description: Le richieste client per l'inserimento di annunci specificano in genere più di un bit rate nella playlist con formato M3U8 variante. Il server manifest genera e restituisce una nuova variante file M3U8 contenente un collegamento M3U8 separato per ogni bit rate. Genera anche un ID gruppo univoco per collegare questi M3U8s.
title: Flussi a bit rate multiplo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Flussi a bit rate multiplo {#multiple-bit-rate-streams}

Le richieste client per l&#39;inserimento di annunci specificano in genere più di un bit rate nella playlist con formato M3U8 variante. Il server manifest genera e restituisce una nuova variante file M3U8 contenente un collegamento M3U8 separato per ogni bit rate. Genera anche un ID gruppo univoco per collegare questi M3U8s.

Il server manifest utilizza le informazioni nella richiesta dell&#39;URL di Bootstrap del client per recuperare la playlist della variante di contenuto. Genera una nuova playlist variante contenente collegamenti del server manifest al contenuto a livello di flusso. Il client li utilizza per creare richieste di inserimento annunci. I collegamenti di contenuto a livello di flusso del server manifest hanno il seguente formato:

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** Il server manifest imposta questo valore in base al tipo di playlist del contenuto: Live/lineare (#EXT-X-PLAYLIST-TYPE:EVENT) o VOD (#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** ID univoco dell&#39;editore per il contenuto specifico fornito nella richiesta di Bootstrap URL.

* **`rendition`** Il server manifest lo imposta in base al valore BANDWIDTH del flusso di contenuti e lo utilizza per corrispondere il bit rate dell&#39;annuncio al bit rate del contenuto. Il bit rate dell’annuncio non può superare il bit rate del contenuto a meno che il rendering dell’annuncio con il bit rate più basso non lo faccia.

* **`groupID`** Il server manifest genera questo valore e lo utilizza per garantire che inserisca gli annunci in modo coerente, indipendentemente dal quale il bit rate esegue il rendering degli annunci da parte del client.

* **`base64-encoded url of the bit rate stream`** Il server manifesto URL-safe base64 codifica l&#39;URL assoluto del flusso di contenuto. Ogni flusso ha il proprio URL.

* **`Query parameters`** Parametri di query forniti nella richiesta URL Bootstrap.

