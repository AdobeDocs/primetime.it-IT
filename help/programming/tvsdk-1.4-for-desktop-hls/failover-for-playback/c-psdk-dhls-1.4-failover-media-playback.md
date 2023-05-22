---
description: Per i contenuti live e video-on-demand (VOD), TVSDK avvia la riproduzione scaricando la playlist associata al bit rate di risoluzione media e scaricando i segmenti multimediali definiti da tale playlist. Seleziona rapidamente la playlist con bitrate ad alta risoluzione e i relativi contenuti e continua il processo di download.
title: Riproduzione e failover dei contenuti multimediali
exl-id: 43a44631-0b45-4f4e-8ec3-d3e1a0d5c71a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---

# Riproduzione e failover dei contenuti multimediali{#media-playback-and-failover}

Per i contenuti live e video-on-demand (VOD), TVSDK avvia la riproduzione scaricando la playlist associata al bit rate di risoluzione media e scaricando i segmenti multimediali definiti da tale playlist. Seleziona rapidamente la playlist con bitrate ad alta risoluzione e i relativi contenuti e continua il processo di download.

## Failover playlist mancante {#section_E6B6A15930894F56A0A8501577B35E7F}

Quando manca un’intera playlist, ad esempio, quando il file M3U8 specificato in un file manifesto di livello superiore non viene scaricato, TVSDK tenta di recuperare. Se non può essere ripristinato, l’applicazione determina il passaggio successivo.

Se manca la playlist associata al bitrate a risoluzione media, TVSDK cerca una playlist variante alla stessa risoluzione. Se trova la stessa risoluzione, inizia a scaricare la playlist delle varianti e i segmenti dalla posizione corrispondente. Se TVSDK non trova la stessa playlist di risoluzione, proverà a scorrere altre playlist con bitrate e le loro varianti. Un bitrate immediatamente inferiore è la prima scelta, quindi la relativa variante e così via. Se tutte le playlist con bitrate inferiore e le relative varianti sono esaurite nel tentativo di trovare una playlist valida, TVSDK passerà al bitrate superiore e da lì verrà conteggiato verso il basso. Se non è possibile trovare una playlist valida, il processo non riesce e il lettore passa allo stato ERROR.

L’applicazione può determinare come gestire questa situazione. Ad esempio, potrebbe essere utile chiudere l’attività del lettore e indirizzare l’utente all’attività catalogo. L&#39;evento di interesse è il `STATUS_CHANGED` e il callback corrispondente è il `onStatusChange` metodo. Di seguito è riportato un codice che controlla se lo stato interno del lettore viene modificato in ERRORE:

Per ulteriori informazioni, vedere `PSDKDemo` file. I listener di eventi sono collegati all’istanza MediaPlayer.

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

Se la rete lato client non funziona, è possibile utilizzare questo codice per verificare.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

L’API fornirà l’URL utilizzato per verificare se la rete lato client è inattiva. Deve essere un URL valido, che restituisce il codice di risposta http 200 nelle richieste http.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

Se setNetworkDownVerificationUrl non è impostato, TVSDK utilizza l&#39;URL MainManifest per impostazione predefinita per determinare se la rete è inattiva.

## Failover del segmento mancante {#section_ED8CF666289042D39E9914D42BDD9BA4}

Quando manca un segmento, ad esempio quando un particolare segmento non riesce a scaricarlo, TVSDK tenta di ripristinarlo tramite diversi tentativi di failover. Se non può essere ripristinato, genera un errore.

Se nel server manca un segmento perché, ad esempio, il file manifesto non è presente, il segmento non può essere scaricato e così via, TVSDK tenta di eseguire il failover tentando le seguenti opzioni:

1. Tentare un failover sullo stesso segmento, alla stessa velocità bit, in un file variante.
1. Passare a una velocità bit alternativa (switch ABR) nello stesso file.
1. Scorre ogni bit rate disponibile in ogni variante disponibile.
1. Ignora il segmento e genera un avviso.

Quando TVSDK non è in grado di ottenere un segmento alternativo, attiva un `CONTENT_ERROR` notifica di errore. Questa notifica contiene una notifica interna con il codice `DOWNLOAD_ERROR` codice. Se il flusso con il problema è una traccia audio alternativa, TVSDK genera il `AUDIO_TRACK_ERROR` notifica di errore.

Se il motore video non è in grado di ottenere segmenti in modo continuo, limita il segmento continuo salta a 5, dopo di che la riproduzione viene interrotta e TVSDK emette un `NATIVE_ERROR` con il codice 5.

>[!NOTE]
>
>I parametri di controllo ABR (Adaptive Bit Rate) non vengono presi in considerazione quando si verifica un failover. Questo perché il meccanismo di failover è progettato per utilizzare come flussi di backup qualsiasi playlist attualmente disponibile, indipendentemente dal suo profilo di bit-rate.
>
>Durante un&#39;operazione di failover può essere presente uno switch di profilo. Se si verifica un errore durante il download di uno dei segmenti della playlist, i parametri di controllo ABR, come la velocità bit minima/massima consentita, vengono ignorati.
