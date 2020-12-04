---
description: L'ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all'applicazione di bilanciare il carico in modo più efficace.
seo-description: L'ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all'applicazione di bilanciare il carico in modo più efficace.
seo-title: Ottimizzazione reindirizzamento HTTP 302
title: Ottimizzazione reindirizzamento HTTP 302
uuid: d3009c6c-320a-4c0f-b6ba-bf6473049823
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---


# Ottimizzazione reindirizzamento HTTP 302 {#http-redirect-optimization}

L&#39;ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all&#39;applicazione di bilanciare il carico in modo più efficace.

Se una richiesta di manifesto principale viene reindirizzata e l’ottimizzazione 302 è abilitata nel lettore, le richieste successive effettuate per le risorse da tale manifesto utilizzeranno la posizione di dominio finale, evitando così ulteriori 302 risposte. Questa funzione è attivata per impostazione predefinita e potete modificare questa impostazione.

>[!IMPORTANT]
>
>Questa funzione è supportata solo nei browser certificati che supportano la proprietà `responseURL` nell&#39;oggetto `XMLHttpRequest`.

Ad Flash, riserva le seguenti informazioni:

* Gli utenti finali devono avere installato  Flash Player Adobe versione 23 o successiva.
* Se l&#39;integrità del flusso è disabilitata, il reindirizzamento 302 è supportato solo sui browser certificati.

## Disattivazione dell&#39;ottimizzazione di reindirizzamento 302 {#disabling-redirect-optimization}

È possibile utilizzare la proprietà useRedirectUrl per abilitare il reindirizzamento 302 (true) o per disabilitare (false).

Ad esempio:

```js
var networkConfiguration = new AdobePSDK.NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = false; 
 
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.networkConfiguration = networkConfiguration;; 
 
player.replaceCurrentResource(mediaResource, config);
```
