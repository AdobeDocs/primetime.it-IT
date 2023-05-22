---
description: L'ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento, consentendo all'applicazione di bilanciare il carico in modo più efficace.
title: Ottimizzazione reindirizzamento HTTP 302
exl-id: fdbdc2b4-6c1a-4ab1-80e2-b5e079ffa906
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 0%

---

# Ottimizzazione reindirizzamento HTTP 302 {#http-redirect-optimization}

L&#39;ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento, consentendo all&#39;applicazione di bilanciare il carico in modo più efficace.

Se una richiesta del manifesto principale viene reindirizzata e l’ottimizzazione 302 è abilitata nel lettore, le richieste successive effettuate per le risorse da tale manifesto utilizzeranno la posizione del dominio finale, evitando ulteriori risposte 302. Questa funzione è attivata per impostazione predefinita e puoi modificarla.

## Disabilita o abilita l&#39;ottimizzazione del reindirizzamento 302 {#section_8977448B268E41D69A8F75B60EB9DA3B}

Utilizza il `useRedirectedUrl` proprietà per attivare il reindirizzamento 302 ( `true`) o disattivato ( `false`).

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
