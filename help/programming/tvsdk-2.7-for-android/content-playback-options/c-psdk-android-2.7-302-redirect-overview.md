---
description: L'ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all'applicazione di bilanciare il carico in modo più efficace.
seo-description: L'ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all'applicazione di bilanciare il carico in modo più efficace.
seo-title: Ottimizzazione reindirizzamento HTTP 302
title: Ottimizzazione reindirizzamento HTTP 302
uuid: 4bee0555-ae46-47c1-a067-206ad7ca8883
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 1%

---


# Ottimizzazione reindirizzamento HTTP 302 {#http-redirect-optimization}

L&#39;ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all&#39;applicazione di bilanciare il carico in modo più efficace.

Se una richiesta di manifesto principale viene reindirizzata e l’ottimizzazione 302 è abilitata nel lettore, le richieste successive effettuate per le risorse da tale manifesto utilizzeranno la posizione di dominio finale, evitando così ulteriori 302 risposte. Questa funzione è attivata per impostazione predefinita e potete modificare questa impostazione.

## Disabilitare o abilitare l&#39;ottimizzazione di reindirizzamento 302 {#section_8977448B268E41D69A8F75B60EB9DA3B}

Utilizzare la proprietà `useRedirectedUrl` per attivare o disattivare il reindirizzamento 302 su ( `true`) o su ( `false`).

<!--<a id="example_888749F70C8A43279D06A29BD68E7E4D"></a>-->

Ad esempio:

```java
// Set useRedirectedUrl property to false 
NetworkConfiguration networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.setUseRedirectedUrl(false); 
 
//Set NetworkConfiguration on MediaPlayerItemConfig 
MediaPlayerItemConfig config = new MediaPlayerItemConfig (); 
config.setNetworkConfiguration(networkConfiguration); 
 
//Use this config when loading the MediaPlayerItem or calling replaceCurrentResource
```

