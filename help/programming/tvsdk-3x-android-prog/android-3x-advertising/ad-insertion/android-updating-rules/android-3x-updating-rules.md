---
description: Puoi utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione degli annunci creativi nelle risposte VAST/VMAP. Puoi anche utilizzare questo file di configurazione per definire le regole di trasformazione dell’URL di origine per le creatività dell’annuncio.
keywords: regole di selezione creativa;AdobeTVSDKConfig;priorità creative;regole di trasformazione
title: Aggiorna le regole di selezione degli annunci creativi
exl-id: da0420a0-6be9-47c8-bdd8-45f0f1860f28
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Panoramica {#update-ad-creative-selection-rules-overview}

Puoi utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione degli annunci creativi nelle risposte VAST/VMAP. Puoi anche utilizzare questo file di configurazione per definire le regole di trasformazione dell’URL di origine per le creatività dell’annuncio.

Quando il lettore video effettua una richiesta a un ad server, la risposta VAST/VMAP di solito include più creativi di annunci ( `MediaFile` elementi ), ciascuno dei quali fornisce un URL per una versione diversa del codec contenitore. In alcuni casi, i creativi degli annunci nella risposta VAST/VMAP forniscono ciascuno un bitrate diverso per l’annuncio. Se desideri specificare la tua priorità e le regole di trasformazione per queste creatività di annunci, puoi farlo in [!DNL AdobeTVSDKConfig.json] file di configurazione.

>[!IMPORTANT]
>
>* Non modificare il nome del file di configurazione TVSDK. Il nome deve rimanere [!DNL AdobeTVSDKConfig.json].
>* Questo file deve essere inserito nel [!DNL assets/] del progetto.
>* La modifica delle tracce audio durante la riproduzione dell’annuncio non cambia la traccia audio. Un lettore non deve consentire agli utenti di modificare la traccia audio durante la riproduzione di un annuncio.
>


È possibile specificare due tipi di regole in [!DNL AdobeTVSDKConfig.json]: *Priorità* regole e *Normalizza* regole.

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

Le regole dell’annuncio vengono specificate utilizzando un file JSON. Il formato del file JSON rimane lo stesso in entrambe le versioni di TVSDK. Tuttavia, in TVSDK v3.0, il file JSON delle regole dell’annuncio deve essere ospitato in una posizione accessibile tramite un URL HTTP. L’applicazione può utilizzare un’istanza di AuditudeSettings:

```
//TVSDK v3.0 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```
