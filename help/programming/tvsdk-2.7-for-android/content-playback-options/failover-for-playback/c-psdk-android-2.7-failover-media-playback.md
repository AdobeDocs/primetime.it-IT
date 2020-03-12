---
description: Per i contenuti multimediali live e video on-demand (VOD), TVSDK avvia la riproduzione scaricando la playlist associata al bitrate a risoluzione intermedia e scarica i segmenti di contenuti multimediali definiti da tale playlist. Seleziona rapidamente la playlist con bitrate ad alta risoluzione e i supporti associati e continua il processo di download.
seo-description: Per i contenuti multimediali live e video on-demand (VOD), TVSDK avvia la riproduzione scaricando la playlist associata al bitrate a risoluzione intermedia e scarica i segmenti di contenuti multimediali definiti da tale playlist. Seleziona rapidamente la playlist con bitrate ad alta risoluzione e i supporti associati e continua il processo di download.
seo-title: Riproduzione e failover dei supporti
title: Riproduzione e failover dei supporti
uuid: 5189cef4-ee09-43b3-ae3d-1052fc535480
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Riproduzione e failover dei supporti {#media-playback-and-failover}

Per i contenuti multimediali live e video on-demand (VOD), TVSDK avvia la riproduzione scaricando la playlist associata al bitrate a risoluzione intermedia e scarica i segmenti di contenuti multimediali definiti da tale playlist. Seleziona rapidamente la playlist con bitrate ad alta risoluzione e i supporti associati e continua il processo di download.

## Failover playlist mancante {#section_4EA0AEFA7FB84FCEA699DFB10B135368}

Quando manca un&#39;intera playlist, ad esempio, quando il file M3U8 specificato in un file manifesto di livello principale non viene scaricato, TVSDK tenta di recuperare. Se non può essere recuperato, l&#39;applicazione determina il passaggio successivo.

Se la playlist associata al bitrate a risoluzione media non è presente, TVSDK cerca una playlist di variante alla stessa risoluzione. Se trova la stessa risoluzione, TVSDK avvia il download della playlist di varianti e dei segmenti dalla posizione corrispondente. Se il lettore non trova la stessa playlist di risoluzione, cercherà di scorrere altre playlist con bitrate e le loro varianti. Un bitrate immediatamente inferiore è la prima scelta, quindi la relativa variante e così via. Se tutte le playlist con bitrate inferiore e le relative varianti sono esaurite nel tentativo di trovare una playlist valida, TVSDK passa al bitrate superiore e conta in basso da lì. Se non è possibile trovare una playlist valida, il processo non riesce e il lettore passa allo stato ERROR.

L&#39;applicazione può determinare come gestire questa situazione. Ad esempio, potrebbe essere utile chiudere l&#39;attività del lettore e indirizzare l&#39;utente all&#39;attività del catalogo. L’evento di interesse è l’ `STATUS_CHANGED` evento e il callback corrispondente è il `onStatusChanged` metodo. Di seguito è riportato il codice che controlla se il lettore modifica il suo stato interno in `ERROR`:

```java
... 
case ERROR: 
getActivity().finish(); // this is where we close the current activity (the Player activity) 
break; 
...
```

## Failover del segmento mancante {#section_D8DF377CCB644D7FB936796DA0CC5A4B}

Quando un segmento non è presente, ad esempio quando un particolare segmento non viene scaricato, TVSDK tenta di eseguire il ripristino attraverso una serie di tentativi di failover. Se non riesce a recuperare, genera un errore.

Se un segmento non è presente sul server perché, ad esempio, il file manifesto non è presente, il segmento non può essere scaricato e così via, TVSDK tenta di eseguire il failover provando le seguenti opzioni:

1. Tentate un failover sullo stesso segmento, allo stesso bitrate, in un file di variante.
1. Passa a un bitrate alternativo (switch ABR) nello stesso file.
1. Scorri ogni bitrate disponibile in ogni variante disponibile.
1. Salta il segmento ed emette un avviso.

Quando TVSDK non è in grado di ottenere un segmento alternativo, attiva una notifica `CONTENT_ERROR` di errore. Questa notifica contiene una notifica interna con il `DOWNLOAD_ERROR` codice. Se lo streaming con il problema è una traccia audio alternativa, TVSDK genera la notifica di `AUDIO_TRACK_ERROR` errore.

Se il motore video non è in grado di ottenere i segmenti in modo continuo, limita l’salita continua a 5, dopo di che la riproduzione viene arrestata e TVSDK emette un errore `NATIVE_ERROR` con il codice 5.

>[!NOTE]
>
>Di seguito sono riportate alcune limitazioni alle quali devi essere a conoscenza: >
>* I parametri di controllo ABR (Adaptive Bit Rate) non vengono presi in considerazione quando si verifica un failover.
>
>  
Questo perché il meccanismo di failover è progettato per utilizzare come flussi di backup uno qualsiasi degli elenchi di riproduzione attualmente disponibili, indipendentemente dal profilo del bit rate.
>* Durante un&#39;operazione di failover, può verificarsi uno switch di profilo.
>
>  
Se si verifica un errore durante il download di uno dei segmenti di playlist, i parametri di controllo ABR come il bit rate minimo/massimo consentito vengono ignorati.


