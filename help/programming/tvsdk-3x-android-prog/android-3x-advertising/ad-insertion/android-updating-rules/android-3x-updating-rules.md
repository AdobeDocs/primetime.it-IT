---
description: Potete utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione di annunci creativi sulle risposte VAST/VMAP. Potete anche utilizzare questo file di configurazione per definire le regole di trasformazione dell'URL di origine per gli annunci creativi.
keywords: creative selection rules;AdobeTVSDKConfig;ad creative priorities;transformation rules
seo-description: Potete utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione di annunci creativi sulle risposte VAST/VMAP. Potete anche utilizzare questo file di configurazione per definire le regole di trasformazione dell'URL di origine per gli annunci creativi.
seo-title: Aggiorna regole di selezione creativa
title: Aggiorna regole di selezione creativa
uuid: 77d8e186-01b5-4d62-8686-28f431d18876
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Panoramica {#update-ad-creative-selection-rules-overview}

Potete utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione di annunci creativi sulle risposte VAST/VMAP. Potete anche utilizzare questo file di configurazione per definire le regole di trasformazione dell&#39;URL di origine per gli annunci creativi.

Quando il lettore video effettua una richiesta a un server di annunci, la risposta VAST/VMAP in genere include più creativi ( `MediaFile` elementi), ciascuno dei quali fornisce un URL a una versione diversa del codec contenitore. In alcuni casi, gli annunci pubblicitari creativi nella risposta VAST/VMAP forniscono per ciascuno un bitrate diverso. Se desiderate specificare la vostra priorità e le regole di trasformazione per queste creative pubblicitarie, potete farlo nel file di configurazione [!DNL AdobeTVSDKConfig.json].

>[!IMPORTANT]
>
>* Non modificate il nome del file di configurazione TVSDK. Il nome deve rimanere [!DNL AdobeTVSDKConfig.json].
>* Questo file deve essere inserito nella cartella [!DNL assets/] del progetto.
>* La modifica delle tracce audio durante la riproduzione di un annuncio non modifica la traccia audio. Un lettore non dovrebbe consentire agli utenti di modificare la traccia audio durante la riproduzione di un annuncio.

>



È possibile specificare due tipi di regole in [!DNL AdobeTVSDKConfig.json]: Regole *Priority* e *Normalize*.

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

Le regole di annuncio vengono specificate utilizzando un file JSON. Il formato del file JSON rimane lo stesso in entrambe le versioni di TVSDK. Tuttavia, in TVSDK v3.0, il file JSON delle regole di annuncio deve essere in hosting su una posizione accessibile tramite un URL HTTP. L’applicazione può utilizzare un’istanza di AuditudeSettings:

```
//TVSDK v3.0 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```
