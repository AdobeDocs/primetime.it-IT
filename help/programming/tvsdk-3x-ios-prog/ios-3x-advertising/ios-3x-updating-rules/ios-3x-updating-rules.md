---
description: Puoi utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione degli annunci creativi nelle risposte VAST/VMAP. Puoi anche utilizzare questo file di configurazione per definire le regole di trasformazione dell’URL di origine per le creatività dell’annuncio.
keywords: regole di selezione creativa;AdobeTVSDKConfig;priorità creative;regole di trasformazione
title: Aggiorna le regole di selezione degli annunci creativi
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Panoramica {#update-ad-creative-selection-rules-overview}

Puoi utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione degli annunci creativi nelle risposte VAST/VMAP. Puoi anche utilizzare questo file di configurazione per definire le regole di trasformazione dell’URL di origine per le creatività dell’annuncio.

Quando il lettore video effettua una richiesta a un ad server, la risposta VAST/VMAP di solito include più creativi di annunci ( `MediaFile` elementi ), ciascuno dei quali fornisce un URL per una versione diversa del codec contenitore. In alcuni casi, i creativi degli annunci nella risposta VAST/VMAP forniscono ciascuno un bitrate diverso per l’annuncio. Se desideri specificare la tua priorità e le regole di trasformazione per queste creatività di annunci, puoi farlo in [!DNL AdobeTVSDKConfig.json] file di configurazione.

>[!IMPORTANT]
>
>* Non modificare il nome del file di configurazione TVSDK. Il nome deve rimanere [!DNL AdobeTVSDKConfig.json].
>* Puoi inserire il file in qualsiasi punto accessibile al pacchetto.
>

È possibile specificare due tipi di regole in [!DNL AdobeTVSDKConfig.json]: *Priorità* regole e *Normalizza* regole.

**[!UICONTROL Disabling Pre-Roll]**

Per disabilitare il pre-roll è necessario modificare i generatori di opportunità predefiniti in modo da non effettuare la chiamata pre-roll. Per impostazione predefinita, TVSDK utilizza i seguenti generatori di opportunità:

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    result.push(new AdSignalingModeOpportunityGenerator()); 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
} 
```

Per disabilitare il pre-roll sui flussi live, questo dovrebbe essere modificato in modo da includere solo SpliceOutOpportunityGenerator:

```
/** 
 * @inheritDoc 
 */ 
override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
    var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
    if (preroll_enabled == true) { 
        result.push(new AdSignalingModeOpportunityGenerator()); 
    } 
    result.push(new SpliceOutOpportunityGenerator()); 
    return result; 
}
```
