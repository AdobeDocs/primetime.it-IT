---
description: Il browser TVSDK supporta attualmente la riproduzione di flussi in cui manifesti e frammenti non contengono estensioni.
title: Flussi illimitati
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# Flussi illimitati{#extensionless-streams}

Il browser TVSDK supporta attualmente la riproduzione di flussi in cui manifesti e frammenti non contengono estensioni.

## Livello di frammento {#section_0E035129501D4A77BBC14192D8A53A86}

Il browser TVSDK analizza i primi byte della risposta per rilevare il tipo di contenuto dei frammenti estensionless. Se non viene rilevato alcun tipo di contenuto valido, il browser TVSDK genererà un errore.

## Livello del manifesto {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

Il browser TVSDK utilizza il parametro `mediaResource.resourceType` passato nel metodo `replaceCurrentResource` per rilevare il tipo di contenuto dell&#39;URL manifesto. Per ulteriori informazioni, vedere la classe `AdobePSDK.MediaPlayer` .

Nel lettore di framework dell&#39;interfaccia utente, puoi specificare il tipo di risorsa nella risorsa multimediale come segue:

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

Se `resourceType` non viene fornito, il framework dell&#39;interfaccia utente determina il tipo di risorsa dall&#39;estensione dell&#39;URL della risorsa, che viene quindi passato al metodo `replaceCurrentResource` .

>[!TIP]
>
>Per un manifesto senza estensione, assicurati che `resourceType` sia sempre passato durante il caricamento di una risorsa in UI Framework.

