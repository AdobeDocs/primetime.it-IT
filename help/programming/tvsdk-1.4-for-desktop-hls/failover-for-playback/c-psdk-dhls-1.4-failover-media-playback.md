---
description: Per i contenuti multimediali live e video su richiesta (VOD), TVSDK avvia la riproduzione scaricando la playlist associata al bitrate a risoluzione intermedia e scaricando i segmenti di contenuti multimediali definiti da tale playlist. Seleziona rapidamente la playlist con bitrate ad alta risoluzione e i supporti associati e continua il processo di download.
seo-description: Per i contenuti multimediali live e video su richiesta (VOD), TVSDK avvia la riproduzione scaricando la playlist associata al bitrate a risoluzione intermedia e scaricando i segmenti di contenuti multimediali definiti da tale playlist. Seleziona rapidamente la playlist con bitrate ad alta risoluzione e i supporti associati e continua il processo di download.
seo-title: Riproduzione e failover dei supporti
title: Riproduzione e failover dei supporti
uuid: 197a6ee0-f1ff-40ac-bd49-eafeae6167d4
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Riproduzione e failover dei supporti{#media-playback-and-failover}

Per i contenuti multimediali live e video su richiesta (VOD), TVSDK avvia la riproduzione scaricando la playlist associata al bitrate a risoluzione intermedia e scaricando i segmenti di contenuti multimediali definiti da tale playlist. Seleziona rapidamente la playlist con bitrate ad alta risoluzione e i supporti associati e continua il processo di download.

## Failover playlist mancante {#section_E6B6A15930894F56A0A8501577B35E7F}

Quando manca un&#39;intera playlist, ad esempio, quando il file M3U8 specificato in un file manifesto di livello principale non viene scaricato, TVSDK tenta di recuperare. Se non può essere recuperato, l&#39;applicazione determina il passaggio successivo.

Se la playlist associata al bitrate a risoluzione media non è presente, TVSDK cerca una playlist di variante alla stessa risoluzione. Se trova la stessa risoluzione, inizia a scaricare la sequenza di riproduzione della variante e i segmenti dalla posizione corrispondente. Se TVSDK non trova la stessa playlist di risoluzione, tenterà di scorrere altre playlist con bitrate e le loro varianti. Un bitrate immediatamente inferiore è la prima scelta, quindi la relativa variante e così via. Se tutte le playlist con bitrate inferiore e le relative varianti sono esaurite nel tentativo di trovare una playlist valida, TVSDK passa al bitrate superiore e conta in basso da lì. Se non è possibile trovare una playlist valida, il processo non riesce e il lettore passa allo stato ERROR.

L&#39;applicazione può determinare come gestire questa situazione. Ad esempio, potrebbe essere utile chiudere l&#39;attività del lettore e indirizzare l&#39;utente all&#39;attività del catalogo. L’evento di interesse è l’ `STATUS_CHANGED` evento e il callback corrispondente è il `onStatusChange` metodo. Di seguito è riportato il codice che controlla se il lettore modifica il proprio stato interno in ERRORE:

Per ulteriori informazioni, vedere il `PSDKDemo` file. I listener di eventi sono collegati all&#39;istanza MediaPlayer.

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

Se la rete lato client è inattiva, potete utilizzare questo codice per verificare.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

L&#39;API fornirà l&#39;URL utilizzato per verificare se la rete lato client è inattiva. Deve essere un URL valido, che restituisce il codice di risposta http 200 sulle richieste http.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

Se setNetworkDownVerificationUrl non è impostato, per impostazione predefinita TVSDK utilizza l’URL MainManifest per configurare se la rete è inattiva.

## Failover del segmento mancante {#section_ED8CF666289042D39E9914D42BDD9BA4}

Quando un segmento non è presente, ad esempio quando un particolare segmento non viene scaricato, TVSDK tenta di eseguire il ripristino attraverso una serie di tentativi di failover. Se non riesce a recuperare, genera un errore.

Se sul server manca un segmento perché, ad esempio, il file manifesto non è presente, il segmento non può essere scaricato e così via, TVSDK tenta di eseguire il failover provando le seguenti opzioni:

1. Tentate un failover sullo stesso segmento, allo stesso bitrate, in un file di variante.
1. Passa a un bitrate alternativo (switch ABR) nello stesso file.
1. Scorri ogni bitrate disponibile in ogni variante disponibile.
1. Salta il segmento ed emette un avviso.

Quando TVSDK non è in grado di ottenere un segmento alternativo, attiva una notifica `CONTENT_ERROR` di errore. Questa notifica contiene una notifica interna con il `DOWNLOAD_ERROR` codice. Se lo streaming con il problema è una traccia audio alternativa, TVSDK genera la notifica di `AUDIO_TRACK_ERROR` errore.

Se il motore video non è in grado di ottenere i segmenti in modo continuo, limita l’salita continua a 5, dopo di che la riproduzione viene arrestata e TVSDK emette un errore `NATIVE_ERROR` con il codice 5.

>[!NOTE]
>
>I parametri di controllo ABR (Adaptive Bit Rate) non vengono presi in considerazione quando si verifica un failover. Ciò è dovuto al fatto che il meccanismo di failover è progettato per utilizzare come flussi di backup uno qualsiasi degli elenchi di riproduzione attualmente disponibili, indipendentemente dal profilo del bit rate.
>
>Durante un&#39;operazione di failover, può verificarsi uno switch di profilo. Se si verifica un errore durante il download di uno dei segmenti di playlist, i parametri di controllo ABR come il bit rate minimo/massimo consentito vengono ignorati.

