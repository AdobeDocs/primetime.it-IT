---
description: L'ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all'applicazione di bilanciare il carico in modo più efficace.
title: Ottimizzazione del reindirizzamento HTTP 302
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---


# Ottimizzazione del reindirizzamento HTTP 302{#http-redirect-optimization}

L&#39;ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all&#39;applicazione di bilanciare il carico in modo più efficace.

Se una richiesta di manifesto principale viene reindirizzata e l’ottimizzazione 302 è abilitata nel lettore, le richieste successive effettuate per le risorse da quel manifesto utilizzeranno la posizione del dominio finale, evitando così ulteriori 302 risposte.

Questa funzione è disabilitata per impostazione predefinita ed è possibile modificarla.

Se abiliti questa funzione, funziona correttamente solo se *all* delle seguenti condizioni è true; in caso contrario, non si verifica alcuna ottimizzazione di reindirizzamento e continuano a verificarsi 302 risposte:

* L&#39;applicazione è stata compilata per Adobe Flash Player 11.8, utilizzando `-swf-version` 21 o versioni successive.
* Gli utenti finali in cui è installato Adobe Flash Player 11.8 o versione successiva.

>[!IMPORTANT]
>
>Per garantire che i cookie vengano passati con le richieste di annunci, disattiva il reindirizzamento 302. Quando è abilitato il reindirizzamento 302, la richiesta di annuncio può essere reindirizzata a un dominio diverso da quello di origine del cookie.

## Disabilita o abilita l&#39;ottimizzazione del reindirizzamento 302 {#section_D6687FC44C61446F878008B629A5FA19}

Utilizza la proprietà `useRedirectedUrl` per attivare (true) o disattivare il reindirizzamento 302 (false).

<!--<a id="example_B886777252B745AAB48B1FCC42C97A25"></a>-->

Ad esempio:

```
// Set useRedirectedUrl property to true 
var networkConfiguration = new NetworkConfiguration(); 
networkConfiguration.useRedirectedUrl = true; 
  
//Set NetworkConfiguration as Metadata: 
var result:Metadata = new Metadata(); 
result.setMetadata(DefaultMetadataKeys.NETWORK_CONFIGURATION_KEY,  
                   networkConfiguration); 
  
var mediaResource = new MediaResource( url, MediaResourceType.HLS, result); 
  
// load the resource 
mediaPlayer.replaceCurrentResource( mediaResource, mediaPlayerItemConfig );
```

