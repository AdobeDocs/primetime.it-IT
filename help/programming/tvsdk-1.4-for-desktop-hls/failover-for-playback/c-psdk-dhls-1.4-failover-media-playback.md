---
description: Per i file multimediali in tempo reale e su richiesta (VOD), TVSDK avvia la riproduzione scaricando la playlist associata al bit rate in risoluzione media e scaricando i segmenti multimediali definiti da tale playlist. Seleziona rapidamente la playlist a bit rate ad alta risoluzione e i supporti associati e continua il processo di download.
title: Riproduzione e failover dei file multimediali
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# Riproduzione e failover dei file multimediali{#media-playback-and-failover}

Per i file multimediali in tempo reale e su richiesta (VOD), TVSDK avvia la riproduzione scaricando la playlist associata al bit rate in risoluzione media e scaricando i segmenti multimediali definiti da tale playlist. Seleziona rapidamente la playlist a bit rate ad alta risoluzione e i supporti associati e continua il processo di download.

## Failover della playlist mancante {#section_E6B6A15930894F56A0A8501577B35E7F}

Quando manca un&#39;intera playlist, ad esempio, quando il file M3U8 specificato in un file manifest di livello superiore non viene scaricato, TVSDK tenta di recuperare. Se non può essere recuperato, l&#39;applicazione determina il passaggio successivo.

Se manca la playlist associata al bit rate a risoluzione media, TVSDK cerca una playlist variante alla stessa risoluzione. Se trova la stessa risoluzione, inizia a scaricare la playlist della variante e i segmenti dalla posizione corrispondente. Se TVSDK non trova la stessa playlist di risoluzione, cercherà di scorrere altre playlist di bitrate e le loro varianti. Un bitrate immediatamente inferiore è la prima scelta, quindi la sua variante, e così via. Se tutte le playlist con bitrate inferiore e le loro varianti sono esaurite nel tentativo di trovare una playlist valida, TVSDK andrà al bitrate superiore e conta giù da lì. Se non è possibile trovare una playlist valida, il processo non riesce e il lettore passa allo stato ERROR.

L&#39;applicazione può determinare come gestire questa situazione. Ad esempio, potrebbe essere utile chiudere l’attività del lettore e indirizzare l’utente all’attività del catalogo. L&#39;evento di interesse è l&#39;evento `STATUS_CHANGED` e il callback corrispondente è il metodo `onStatusChange` . Ecco un codice che controlla se il lettore modifica il proprio stato interno in ERRORE:

Per ulteriori informazioni, consulta il file `PSDKDemo` . I listener di eventi sono collegati all&#39;istanza MediaPlayer.

```
case MediaPlayerStatus.ERROR: 
Alert.show(event.error.toString(), “Error occurred”); 
break;
```

Se la rete lato client è inattiva, puoi utilizzare questo codice per verificare.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

L’API fornirà l’URL utilizzato per verificare se la rete lato client è inattiva. Deve essere un URL valido, che restituisce il codice di risposta http 200 sulle richieste http.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

Se setNetworkDownVerificationUrl non è impostato, per impostazione predefinita TVSDK utilizza l&#39;URL MainManifest per configurare se la rete è inattiva.

## Failover dei segmenti mancante {#section_ED8CF666289042D39E9914D42BDD9BA4}

Quando manca un segmento, ad esempio quando un particolare segmento non viene scaricato, TVSDK tenta di eseguire il ripristino tramite diversi tentativi di failover. Se non è in grado di eseguire il ripristino, viene generato un errore.

Se sul server manca un segmento perché, ad esempio, il file manifesto non è presente, il segmento non può essere scaricato e così via, TVSDK tenta di eseguire il failover provando le seguenti opzioni:

1. Prova un failover sullo stesso segmento, allo stesso bit rate, in un file variante.
1. Passa a un bit rate alternativo (interruttore ABR) nello stesso file.
1. Scorrere ogni bit rate disponibile in ogni variante disponibile.
1. Ignora il segmento ed emette un avviso.

Quando TVSDK non è in grado di ottenere un segmento alternativo, attiva una notifica di errore `CONTENT_ERROR`. Questa notifica contiene una notifica interna con il codice `DOWNLOAD_ERROR` . Se lo streaming con il problema è una traccia audio alternativa, TVSDK genera la notifica di errore `AUDIO_TRACK_ERROR`.

Se il motore video non è in grado di ottenere continuamente i segmenti, limita l’salto continuo del segmento a 5, dopo di che la riproduzione viene interrotta e TVSDK rilascia un `NATIVE_ERROR` con il codice 5.

>[!NOTE]
>
>I parametri di controllo del bit rate adattivo (ABR) non vengono presi in considerazione quando si verifica un failover. Questo perché il meccanismo di failover è progettato per utilizzare come flussi di backup qualsiasi playlist attualmente disponibile, indipendentemente dal loro profilo bit-rate.
>
>Durante un&#39;operazione di failover, può essere presente uno switch di profilo. Se si verifica un errore durante il download di uno dei segmenti della playlist, i parametri di controllo ABR come il bit rate minimo/massimo consentito vengono ignorati.

