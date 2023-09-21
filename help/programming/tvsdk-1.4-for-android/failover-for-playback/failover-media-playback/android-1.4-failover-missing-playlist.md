---
description: Quando manca un’intera playlist, ad esempio, quando il file M3U8 specificato in un file manifesto di livello superiore non viene scaricato, TVSDK tenta di recuperare. Se non è possibile ripristinarlo, l'applicazione determina il passaggio successivo.
title: Failover playlist mancante
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Failover playlist mancante{#missing-playlist-failover}

Quando manca un’intera playlist, ad esempio, quando il file M3U8 specificato in un file manifesto di livello superiore non viene scaricato, TVSDK tenta di recuperare. Se non è possibile ripristinarlo, l&#39;applicazione determina il passaggio successivo.

Se manca la playlist associata al bitrate a risoluzione media, TVSDK cerca una playlist variante alla stessa risoluzione. Se trova la stessa risoluzione, inizia a scaricare la playlist delle varianti e i segmenti dalla posizione corrispondente. Se TVSDK non trova la stessa playlist di risoluzione, proverà a scorrere altre playlist con bitrate e le loro varianti. Un bitrate immediatamente inferiore è la prima scelta, quindi la relativa variante e così via. Se tutte le playlist con bitrate inferiore e le relative varianti sono esaurite nel tentativo di trovare una playlist valida, TVSDK passerà al bitrate superiore e da lì verrà conteggiato verso il basso. Se non è possibile trovare una playlist valida, il processo non riesce e il lettore passa allo stato ERROR.

L’applicazione può determinare come gestire questa situazione. Ad esempio, potrebbe essere utile chiudere l’attività del lettore e indirizzare l’utente all’attività catalogo. L&#39;evento di interesse è il `STATE_CHANGED` e il callback corrispondente è il `onStateChanged` metodo. Di seguito è riportato un codice che controlla se lo stato interno del lettore viene modificato in ERRORE:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

Per ulteriori informazioni, vedere [!DNL PlayerFragment.java] nell’SDK:

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
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
