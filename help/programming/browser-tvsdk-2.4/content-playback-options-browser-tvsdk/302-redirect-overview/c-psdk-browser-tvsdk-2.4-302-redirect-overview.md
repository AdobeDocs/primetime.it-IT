---
description: L'ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento, consentendo all'applicazione di bilanciare il carico in modo più efficace.
title: Ottimizzazione reindirizzamento HTTP 302
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Ottimizzazione reindirizzamento HTTP 302 {#http-redirect-optimization}

L&#39;ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento, consentendo all&#39;applicazione di bilanciare il carico in modo più efficace.

Se una richiesta del manifesto principale viene reindirizzata e l’ottimizzazione 302 è abilitata nel lettore, le richieste successive effettuate per le risorse da tale manifesto utilizzeranno la posizione del dominio finale, evitando ulteriori risposte 302. Questa funzione è attivata per impostazione predefinita e puoi modificarla.

>[!IMPORTANT]
>
>Questa funzione è supportata solo nei browser certificati che supportano `responseURL` proprietà in `XMLHttpRequest` oggetto.

Per il fallback di Flash, ricorda le seguenti informazioni:

* Gli utenti finali devono avere installato Adobe Flash Player versione 23 o successiva.
* Se l&#39;integrità del flusso è disabilitata, il reindirizzamento 302 è supportato solo nei browser certificati.

## Disabilitazione dell’ottimizzazione del reindirizzamento 302 {#disabling-redirect-optimization}

È possibile utilizzare la proprietà useRedirectedUrl per abilitare il reindirizzamento 302 (true) o disabilitare (false).

Ad esempio:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
