---
description: Per i file multimediali live e VOD, Browser TVSDK avvia la riproduzione scaricando la playlist associata al bitrate della risoluzione media e quindi scaricando i segmenti del file multimediale con bitrate della risoluzione media definito dalla playlist.
seo-description: Per i file multimediali live e VOD, Browser TVSDK avvia la riproduzione scaricando la playlist associata al bitrate della risoluzione media e quindi scaricando i segmenti del file multimediale con bitrate della risoluzione media definito dalla playlist.
seo-title: Riproduzione multimediale
title: Riproduzione multimediale
uuid: 454f84fe-8077-4f37-8e62-1d6ba0fcde27
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Riproduzione multimediale {#media-playback}

Per i file multimediali live e VOD, Browser TVSDK avvia la riproduzione scaricando la playlist associata al bitrate della risoluzione media e quindi scaricando i segmenti del file multimediale con bitrate della risoluzione media definito dalla playlist.

Il browser TVSDK seleziona rapidamente la playlist con bitrate ad alta risoluzione e i relativi contenuti multimediali e continua il processo di download.

## Failover playlist mancante {#section_81A5822C108449E1A0E94A6E25DE9E8E}

Se manca un&#39;intera playlist, ad esempio, quando il file M3U8 specificato in un file manifesto di livello principale non viene scaricato, il browser TVSDK tenta di recuperare. Se non può essere recuperato, l&#39;applicazione determina il passaggio successivo.

Se la playlist associata al bitrate a risoluzione media non è presente, il browser TVSDK cerca una playlist di variante alla stessa risoluzione. Se trova la stessa risoluzione, inizia a scaricare la sequenza di riproduzione della variante e i segmenti dalla posizione corrispondente. Se il browser TVSDK non trova la stessa playlist di risoluzione, tenterà di scorrere altre playlist con bitrate e le loro varianti. Un bitrate immediatamente inferiore è la prima scelta, quindi la relativa variante e così via. Se tutte le playlist con bitrate inferiore e le relative varianti sono esaurite nel tentativo di trovare una playlist valida, Browser TVSDK passerà al bitrate superiore e conta verso il basso da lì. Se non è possibile trovare una playlist valida, il processo non riesce e il lettore passa allo stato ERROR.

L&#39;applicazione può determinare come gestire questa situazione. Ad esempio, potrebbe essere utile chiudere l&#39;attività del lettore e indirizzare l&#39;utente all&#39;attività del catalogo. L’evento di interesse è l’evento stato o stato modificato e il callback corrispondente è il metodo attivato modificato di stato. Di seguito è riportato il codice che controlla se il lettore modifica il proprio stato interno in ERRORE:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
