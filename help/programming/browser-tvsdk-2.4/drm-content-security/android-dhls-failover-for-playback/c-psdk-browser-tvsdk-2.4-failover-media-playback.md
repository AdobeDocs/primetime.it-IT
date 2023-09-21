---
description: Per i file multimediali in diretta e VOD, il browser TVSDK avvia la riproduzione scaricando la playlist associata al bitrate di risoluzione media e quindi scaricando i segmenti dei file multimediali con bitrate di risoluzione media definiti dalla playlist.
title: Riproduzione di contenuti multimediali
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Riproduzione di contenuti multimediali {#media-playback}

Per i file multimediali in diretta e VOD, il browser TVSDK avvia la riproduzione scaricando la playlist associata al bitrate di risoluzione media e quindi scaricando i segmenti dei file multimediali con bitrate di risoluzione media definiti dalla playlist.

Browser TVSDK seleziona rapidamente la playlist con bitrate ad alta risoluzione e i relativi supporti e continua il processo di download.

## Failover playlist mancante {#section_81A5822C108449E1A0E94A6E25DE9E8E}

Quando manca un’intera playlist, ad esempio, quando il file M3U8 specificato in un file manifesto di livello superiore non viene scaricato, TVSDK del browser tenta di ripristinarlo. Se non può essere ripristinato, l’applicazione determina il passaggio successivo.

Se manca la playlist associata al bitrate a risoluzione media, il browser TVSDK cerca una playlist variante alla stessa risoluzione. Se trova la stessa risoluzione, inizia a scaricare la playlist delle varianti e i segmenti dalla posizione corrispondente. Se il TVSDK del browser non trova la stessa playlist di risoluzione, proverà a passare da un’altra playlist con bitrate e le relative varianti. Un bitrate immediatamente inferiore è la prima scelta, quindi la relativa variante e così via. Se tutte le playlist con bitrate inferiore e le relative varianti sono esaurite nel tentativo di trovare una playlist valida, il TVSDK del browser passerà al bitrate superiore e da lì in poi eseguirà il conto alla rovescia. Se non è possibile trovare una playlist valida, il processo non riesce e il lettore passa allo stato ERROR.

L’applicazione può determinare come gestire questa situazione. Ad esempio, potrebbe essere utile chiudere l’attività del lettore e indirizzare l’utente all’attività catalogo. L&#39;evento di interesse è l&#39;evento stato o stato modificato e il callback corrispondente è il metodo on status changed. Di seguito è riportato un codice che controlla se lo stato interno del lettore viene modificato in ERRORE:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
