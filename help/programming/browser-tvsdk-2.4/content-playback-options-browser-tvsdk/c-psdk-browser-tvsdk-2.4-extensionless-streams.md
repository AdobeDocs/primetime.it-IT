---
description: Browser TVSDK supporta attualmente la riproduzione di flussi in cui i manifesti e i frammenti non contengono estensioni.
seo-description: Browser TVSDK supporta attualmente la riproduzione di flussi in cui i manifesti e i frammenti non contengono estensioni.
seo-title: Flussi illimitati
title: Flussi illimitati
uuid: c69ba62b-a940-4211-920d-2e559849fd6d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Flussi illimitati{#extensionless-streams}

Browser TVSDK supporta attualmente la riproduzione di flussi in cui i manifesti e i frammenti non contengono estensioni.

## Livello frammento {#section_0E035129501D4A77BBC14192D8A53A86}

Browser TVSDK analizza i primi byte della risposta per rilevare il tipo di contenuto dei frammenti estensionless. Se non viene rilevato alcun tipo di contenuto valido, il browser TVSDK genererà un errore.

## Livello manifesto {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

Browser TVSDK usa il `mediaResource.resourceType` parametro passato nel `replaceCurrentResource` metodo per rilevare il tipo di contenuto dell&#39;URL del manifesto. Per ulteriori informazioni, vedere la `AdobePSDK.MediaPlayer` classe.

Nel lettore di UI Framework è possibile specificare il tipo di risorsa nella risorsa multimediale come segue:

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

Se non `resourceType` viene fornito, il framework di interfaccia utente determina il tipo di risorsa dall&#39;estensione URL risorsa, che viene quindi passata al `replaceCurrentResource` metodo.

>[!TIP]
>
>Per un manifesto senza estensione, accertati che `resourceType` venga sempre passato durante il caricamento di una risorsa in UI Framework.

