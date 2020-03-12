---
description: L'ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all'applicazione di bilanciare il carico in modo più efficace.
seo-description: L'ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all'applicazione di bilanciare il carico in modo più efficace.
seo-title: Ottimizzazione reindirizzamento HTTP 302
title: Ottimizzazione reindirizzamento HTTP 302
uuid: 58593d5f-a639-4d87-9589-dba6b2dbba38
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Ottimizzazione reindirizzamento HTTP 302{#http-redirect-optimization}

L&#39;ottimizzazione del reindirizzamento 302 riduce al minimo il numero di risposte di reindirizzamento 302, consentendo all&#39;applicazione di bilanciare il carico in modo più efficace.

Se una richiesta di manifesto principale viene reindirizzata e l’ottimizzazione 302 è abilitata nel lettore, le richieste successive effettuate per le risorse da tale manifesto utilizzeranno la posizione di dominio finale, evitando così ulteriori 302 risposte.

Questa funzione è disattivata per impostazione predefinita e potete modificare questa impostazione.

Se attivate questa funzione, funziona correttamente solo se *tutte* le seguenti condizioni sono soddisfatte; in caso contrario, non si verifica alcuna ottimizzazione di reindirizzamento e continuano a verificarsi 302 risposte:

* L’applicazione è stata compilata per Adobe Flash Player 11.8, con `-swf-version` 21 o versione successiva.
* Gli utenti finali dispongono di Adobe Flash Player 11.8 o versione successiva installato.

>[!IMPORTANT]
>
>Per assicurarsi che i cookie vengano passati con le richieste di annunci, disattivate il reindirizzamento 302. Quando il reindirizzamento 302 è abilitato, la richiesta di annuncio potrebbe essere reindirizzata a un dominio diverso da quello da cui il cookie ha avuto origine.

## Disabilitare o abilitare l&#39;ottimizzazione di reindirizzamento 302 {#section_D6687FC44C61446F878008B629A5FA19}

Utilizzare la `useRedirectedUrl` proprietà per attivare (true) o disattivare (false) il reindirizzamento 302.

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

