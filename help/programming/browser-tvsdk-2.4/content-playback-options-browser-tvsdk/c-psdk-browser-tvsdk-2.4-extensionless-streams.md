---
description: Il TVSDK del browser attualmente supporta la riproduzione di flussi in cui i manifesti e i frammenti non contengono estensioni.
title: Flussi senza estensione
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Flussi senza estensione{#extensionless-streams}

Il TVSDK del browser attualmente supporta la riproduzione di flussi in cui i manifesti e i frammenti non contengono estensioni.

## Livello di frammento {#section_0E035129501D4A77BBC14192D8A53A86}

Il TVSDK del browser analizza i primi byte della risposta per rilevare il tipo di contenuto dei frammenti senza estensione. Se non viene rilevato alcun tipo di contenuto valido, la funzione TVSDK del browser genererà un errore.

## Livello manifesto {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

TVSDK del browser utilizza `mediaResource.resourceType` parametro passato nel `replaceCurrentResource` per rilevare il tipo di contenuto dell’URL del manifesto. Per ulteriori informazioni, vedere `AdobePSDK.MediaPlayer` classe.

Nel lettore del framework dell’interfaccia utente, puoi specificare il tipo di risorsa nella risorsa multimediale come segue:

```js
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
  player: { 
    mediaResource: { 
      resourceUrl:'Specify Resource Url', 
      resourceType: ‘Specify Resource Type. Refer AdobePSDK.MediaResourceType' 
    } 
  } 
}); 
```

Se `resourceType` non viene fornito, il Framework dell’interfaccia utente determina il tipo di risorsa dall’estensione URL della risorsa, che viene quindi passata a `replaceCurrentResource` metodo.

>[!TIP]
>
>Per il manifesto senza estensione, assicurati che `resourceType` viene sempre passato durante il caricamento di una risorsa nel Framework dell’interfaccia utente.
