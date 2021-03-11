---
description: Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione a distanza di contenuti multimediali riprodotti localmente.
title: Riproduzione e failover
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# Riproduzione e failover {#playback-and-failover}

Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un visualizzatore impedisce la riproduzione a distanza di contenuti multimediali riprodotti localmente.

Primetime non è in grado di proteggere da guasti come un&#39;interruzione dell&#39;ISP o una disconnessione del cavo. Tuttavia, lo streaming Primetime fornisce una protezione di failover per proteggere la riproduzione da alcuni guasti o guasti operativi del server remoto, offrendo ai visualizzatori un&#39;esperienza migliore. Browser TVSDK implementa la protezione del failover per ridurre al minimo le interruzioni di riproduzione e ottenere una riproduzione senza soluzione di continuità nonostante i problemi di trasmissione. Il lettore video passa automaticamente a un set di file multimediali di backup quando non sono disponibili interi rendering o frammenti.

## Riproduzione multimediale {#media-playback}

Per i file multimediali in diretta e VOD, il browser TVSDK avvia la riproduzione scaricando la playlist associata al bit rate in risoluzione media e quindi scaricando i segmenti del bit rate in risoluzione media definito dalla playlist.

Browser TVSDK seleziona rapidamente la playlist a bit rate ad alta risoluzione e i relativi file multimediali associati e continua il processo di download.

## Failover della playlist mancante {#section_81A5822C108449E1A0E94A6E25DE9E8E}

Quando manca un&#39;intera playlist, ad esempio, quando il file M3U8 specificato in un file manifest di livello superiore non viene scaricato, il browser TVSDK tenta di recuperare. Se non può essere recuperato, l&#39;applicazione determina il passaggio successivo.

Se la playlist associata al bit rate a risoluzione media è mancante, il browser TVSDK cerca una playlist variante alla stessa risoluzione. Se trova la stessa risoluzione, inizia a scaricare la playlist della variante e i segmenti dalla posizione corrispondente. Se il browser TVSDK non trova la stessa playlist di risoluzione, proverà a scorrere altre playlist di bitrate e le loro varianti. Un bitrate immediatamente inferiore è la prima scelta, quindi la sua variante, e così via. Se tutte le playlist con bitrate inferiore e le loro varianti sono esaurite nel tentativo di trovare una playlist valida, Browser TVSDK andrà al bitrate superiore e conta giù da lì. Se non è possibile trovare una playlist valida, il processo non riesce e il lettore passa allo stato ERROR.

L&#39;applicazione può determinare come gestire questa situazione. Ad esempio, potrebbe essere utile chiudere l’attività del lettore e indirizzare l’utente all’attività del catalogo. L&#39;evento di interesse è l&#39;evento di stato o stato modificato e il callback corrispondente è il metodo di modifica dello stato di attivazione. Ecco un codice che controlla se il lettore modifica il proprio stato interno in ERRORE:

```js
case AdobePSDK.MediaPlayerStatus.ERROR:  
var errorDesc = event.metadata.getValue('DESCRIPTION'); 
console.log(errorDesc); 
break; 
```
