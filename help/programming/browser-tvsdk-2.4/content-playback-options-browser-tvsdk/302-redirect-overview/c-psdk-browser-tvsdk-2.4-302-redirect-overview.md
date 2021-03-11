---
description: L'ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all'applicazione di bilanciare il carico in modo più efficace.
title: Ottimizzazione del reindirizzamento HTTP 302
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---


# Ottimizzazione del reindirizzamento HTTP 302 {#http-redirect-optimization}

L&#39;ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all&#39;applicazione di bilanciare il carico in modo più efficace.

Se una richiesta di manifesto principale viene reindirizzata e l’ottimizzazione 302 è abilitata nel lettore, le richieste successive effettuate per le risorse da quel manifesto utilizzeranno la posizione del dominio finale, evitando così ulteriori 302 risposte. Questa funzione è attivata per impostazione predefinita ed è possibile modificarla.

>[!IMPORTANT]
>
>Questa funzione è supportata solo nei browser certificati che supportano la proprietà `responseURL` nell&#39;oggetto `XMLHttpRequest` .

Per Flash, ricorda le seguenti informazioni:

* Gli utenti finali devono avere installato Adobe Flash Player versione 23 o successiva.
* Se l’integrità del flusso è disabilitata, il reindirizzamento 302 è supportato solo sui browser certificati.

## Disabilitazione dell&#39;ottimizzazione del reindirizzamento 302 {#disabling-redirect-optimization}

È possibile utilizzare la proprietà useReindirizzaUrl per abilitare il reindirizzamento 302 (true) o disabilitare (false).

Ad esempio:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
