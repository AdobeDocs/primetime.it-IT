---
description: Quando manca un'intera playlist, ad esempio, quando il file M3U8 specificato in un file manifest di livello superiore non viene scaricato, TVSDK tenta di recuperare. Se non è possibile eseguire il ripristino, l'applicazione determina il passaggio successivo.
title: Failover della playlist mancante
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# Failover della playlist mancante{#missing-playlist-failover}

Quando manca un&#39;intera playlist, ad esempio, quando il file M3U8 specificato in un file manifest di livello superiore non viene scaricato, TVSDK tenta di recuperare. Se non è possibile eseguire il ripristino, l&#39;applicazione determina il passaggio successivo.

Se manca la playlist associata al bit rate a risoluzione media, TVSDK cerca una playlist variante alla stessa risoluzione. Se trova la stessa risoluzione, inizia a scaricare la playlist della variante e i segmenti dalla posizione corrispondente. Se TVSDK non trova la stessa playlist di risoluzione, cercherà di scorrere altre playlist di bitrate e le loro varianti. Un bitrate immediatamente inferiore è la prima scelta, quindi la sua variante, e così via. Se tutte le playlist con bitrate inferiore e le loro varianti sono esaurite nel tentativo di trovare una playlist valida, TVSDK andrà al bitrate superiore e conta giù da lì. Se non è possibile trovare una playlist valida, il processo non riesce e il lettore passa allo stato ERROR.

L&#39;applicazione può determinare come gestire questa situazione. Ad esempio, potrebbe essere utile chiudere l’attività del lettore e indirizzare l’utente all’attività del catalogo. L&#39;evento di interesse è l&#39;evento `STATE_CHANGED` e il callback corrispondente è il metodo `onStateChanged` . Ecco un codice che controlla se il lettore modifica il proprio stato interno in ERRORE:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

Per ulteriori informazioni, consulta il file [!DNL PlayerFragment.java] nell’SDK:

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
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
