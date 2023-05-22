---
description: Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un utente fa sì che la riproduzione remota possa non avere la qualità dei contenuti multimediali riprodotti localmente.
title: Riproduzione e failover
exl-id: 8316dfb8-3a2e-4057-a3d7-e3d8860e5bd4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Riproduzione e failover {#playback-and-failover}

Lo streaming via Internet richiede una connessione costante e stabile per riprodurre un flusso da un server remoto. Tuttavia, la variabilità della connessione Internet o della riproduzione in streaming di un utente fa sì che la riproduzione remota possa non avere la qualità dei contenuti multimediali riprodotti localmente.

Primetime non è in grado di proteggere da errori quali un&#39;interruzione del servizio ISP o la disconnessione di un cavo. Tuttavia, lo streaming di Primetime offre protezione da failover per proteggere la riproduzione da determinati guasti del server remoto o da errori operativi, migliorando l&#39;esperienza dei visualizzatori. Browser TVSDK implementa la protezione di failover per ridurre al minimo le interruzioni della riproduzione e ottenere una riproduzione ottimale nonostante i problemi di trasmissione. Il lettore video passa automaticamente a un set di supporti di backup quando non sono disponibili rappresentazioni o frammenti interi.

## Riproduzione di contenuti multimediali {#media-playback}

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
