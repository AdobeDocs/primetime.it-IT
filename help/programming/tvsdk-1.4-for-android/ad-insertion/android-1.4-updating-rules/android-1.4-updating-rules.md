---
description: Puoi utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione creativa degli annunci sulle risposte VAST/VMAP. Puoi anche utilizzare questo file di configurazione per definire le regole di trasformazione dell’URL di origine per gli inserzionisti.
keywords: regole di selezione creativa;AdobeTVSDKConfig;priorità creative;regole di trasformazione
title: Aggiornamento delle regole di selezione pubblicitaria
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---


# Panoramica {#updating-ad-creative-selection-rules-overview}

Puoi utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione creativa degli annunci sulle risposte VAST/VMAP. Puoi anche utilizzare questo file di configurazione per definire le regole di trasformazione dell’URL di origine per gli inserzionisti.

Quando il lettore video effettua una richiesta a un server di annunci, la risposta VAST/VMAP di solito include più creativi di annunci ( `MediaFile` elementi), ciascuno dei quali fornisce un URL a una versione diversa del codec contenitore. In alcuni casi, i creativi di annunci nella risposta VAST/VMAP forniscono ciascuno un bitrate diverso per l&#39;annuncio. Se desideri specificare la tua priorità e le regole di trasformazione per questi creativi di annunci, puoi farlo nel file di configurazione [!DNL AdobeTVSDKConfig.json] .

>[!IMPORTANT]
>
>* Non modificare il nome del file di configurazione TVSDK. Il nome deve rimanere [!DNL AdobeTVSDKConfig.json].
>* Il file deve trovarsi nella cartella [!DNL assets/] del progetto.

>



Puoi specificare due tipi di regole in [!DNL AdobeTVSDKConfig.json]: Regole *Priorità* e regole *Normalizza*.

## Disabilitazione del pre-roll {#disabling-preroll}

Per disabilitare il pre-roll è necessario modificare i generatori di opportunità predefiniti per non effettuare la chiamata pre-roll. Per impostazione predefinita, TVSDK utilizza i seguenti generatori di opportunità:

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

Per disabilitare il pre-roll sui flussi in diretta, questo dovrebbe cambiare per includere solo il SpliceOutOpportunityGenerator:

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

