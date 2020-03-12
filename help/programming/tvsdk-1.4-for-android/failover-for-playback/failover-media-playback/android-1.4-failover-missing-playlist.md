---
description: Quando manca un'intera playlist, ad esempio, quando il file M3U8 specificato in un file manifesto di livello principale non viene scaricato, TVSDK tenta di recuperare. Se non è possibile eseguire il ripristino, l'applicazione determina il passaggio successivo.
seo-description: Quando manca un'intera playlist, ad esempio, quando il file M3U8 specificato in un file manifesto di livello principale non viene scaricato, TVSDK tenta di recuperare. Se non è possibile eseguire il ripristino, l'applicazione determina il passaggio successivo.
seo-title: Failover playlist mancante
title: Failover playlist mancante
uuid: 91a537f3-3e69-4669-8f84-0292c19ac209
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Failover playlist mancante{#missing-playlist-failover}

Quando manca un&#39;intera playlist, ad esempio, quando il file M3U8 specificato in un file manifesto di livello principale non viene scaricato, TVSDK tenta di recuperare. Se non è possibile eseguire il ripristino, l&#39;applicazione determina il passaggio successivo.

Se la playlist associata al bitrate a risoluzione media non è presente, TVSDK cerca una playlist di variante alla stessa risoluzione. Se trova la stessa risoluzione, inizia a scaricare la sequenza di riproduzione della variante e i segmenti dalla posizione corrispondente. Se TVSDK non trova la stessa playlist di risoluzione, tenterà di scorrere altre playlist con bitrate e le loro varianti. Un bitrate immediatamente inferiore è la prima scelta, quindi la relativa variante e così via. Se tutte le playlist con bitrate inferiore e le relative varianti sono esaurite nel tentativo di trovare una playlist valida, TVSDK passa al bitrate superiore e conta in basso da lì. Se non è possibile trovare una playlist valida, il processo non riesce e il lettore passa allo stato ERROR.

L&#39;applicazione può determinare come gestire questa situazione. Ad esempio, potrebbe essere utile chiudere l&#39;attività del lettore e indirizzare l&#39;utente all&#39;attività del catalogo. L’evento di interesse è l’ `STATE_CHANGED` evento e il callback corrispondente è il `onStateChanged` metodo. Di seguito è riportato il codice che controlla se il lettore modifica il proprio stato interno in ERRORE:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

Per ulteriori informazioni, consulta il [!DNL PlayerFragment.java] file nell’SDK:

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
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
