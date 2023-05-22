---
description: L'ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento, consentendo all'applicazione di bilanciare il carico in modo più efficace.
title: Ottimizzazione reindirizzamento HTTP 302
exl-id: 9b9d98ae-a509-47dc-a5ac-6be9b0f214c1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Ottimizzazione reindirizzamento HTTP 302{#http-redirect-optimization}

L&#39;ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento, consentendo all&#39;applicazione di bilanciare il carico in modo più efficace.

Se una richiesta del manifesto principale viene reindirizzata e l’ottimizzazione 302 è abilitata nel lettore, le richieste successive effettuate per le risorse da tale manifesto utilizzeranno la posizione del dominio finale, evitando ulteriori risposte 302.

Questa funzione è disabilitata per impostazione predefinita ed è possibile modificare questa impostazione.

Se abiliti questa funzione, questa funziona correttamente solo se *tutto* delle seguenti condizioni sono vere; in caso contrario, non si verifica alcuna ottimizzazione di reindirizzamento e continuano a verificarsi risposte 302:

* L&#39;applicazione è stata compilata per l&#39;Adobe Flash Player 11.8, utilizzando `-swf-version` 21 o superiore.
* Gli utenti finali hanno installato Adobe Flash Player 11.8 o versione successiva.

>[!IMPORTANT]
>
>Per garantire che i cookie vengano passati con le richieste di annunci, disabilita il reindirizzamento 302. Quando è abilitato il reindirizzamento 302, la richiesta dell’annuncio potrebbe essere reindirizzata a un dominio diverso da quello da cui ha origine il cookie.

## Disabilita o abilita l&#39;ottimizzazione del reindirizzamento 302 {#section_D6687FC44C61446F878008B629A5FA19}

Utilizza il `useRedirectedUrl` per attivare o disattivare il reindirizzamento 302 (true).

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
