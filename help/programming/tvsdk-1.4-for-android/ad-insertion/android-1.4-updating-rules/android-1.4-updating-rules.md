---
description: Potete utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione di annunci creativi sulle risposte VAST/VMAP. Potete anche utilizzare questo file di configurazione per definire le regole di trasformazione dell'URL di origine per gli annunci creativi.
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
seo-description: Potete utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione di annunci creativi sulle risposte VAST/VMAP. Potete anche utilizzare questo file di configurazione per definire le regole di trasformazione dell'URL di origine per gli annunci creativi.
seo-title: Aggiornamento delle regole di selezione di annunci pubblicitari
title: Aggiornamento delle regole di selezione di annunci pubblicitari
uuid: 84cc13d1-21a3-456b-95c8-200bfec7b453
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Panoramica {#updating-ad-creative-selection-rules-overview}

Potete utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione di annunci creativi sulle risposte VAST/VMAP. Potete anche utilizzare questo file di configurazione per definire le regole di trasformazione dell&#39;URL di origine per gli annunci creativi.

Quando il lettore video effettua una richiesta a un server di annunci, la risposta VAST/VMAP in genere include più creativi ( `MediaFile` elementi) di annunci, ciascuno dei quali fornisce un URL a una versione contenitore-codec diversa. In alcuni casi, gli annunci pubblicitari creativi nella risposta VAST/VMAP forniscono per ciascuno un bitrate diverso. Se desiderate specificare la vostra priorità e le regole di trasformazione per queste creative pubblicitarie, potete farlo nel file di [!DNL AdobeTVSDKConfig.json] configurazione.

>[!IMPORTANT]
>
>* Non modificate il nome del file di configurazione TVSDK. Il nome deve restare [!DNL AdobeTVSDKConfig.json].
>* Questo file deve essere inserito nella [!DNL assets/] cartella del progetto.
>



È possibile specificare due tipi di regole in [!DNL AdobeTVSDKConfig.json]: Regole *prioritarie* e regole *normalizzate* .

## Disattivazione del pre-rollio {#disabling-preroll}

Per disattivare il pre-roll sarà necessario modificare i generatori di opportunità predefiniti per non effettuare la chiamata pre-roll. Per impostazione predefinita, TVSDK utilizza i seguenti generatori di opportunità:

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

Per disattivare il pre-roll sui flussi live, questo dovrebbe essere modificato in modo da includere solo SpliceOutOpportunityGenerator:

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

