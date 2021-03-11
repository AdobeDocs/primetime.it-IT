---
description: Puoi utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione creativa degli annunci sulle risposte VAST/VMAP. Puoi anche utilizzare questo file di configurazione per definire le regole di trasformazione dell’URL di origine per gli inserzionisti.
keywords: regole di selezione creativa;AdobeTVSDKConfig;priorità creative;regole di trasformazione
title: Aggiorna le regole di selezione creativa
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---


# Panoramica {#update-ad-creative-selection-rules-overview}

Puoi utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione creativa degli annunci sulle risposte VAST/VMAP. Puoi anche utilizzare questo file di configurazione per definire le regole di trasformazione dell’URL di origine per gli inserzionisti.

Quando il lettore video effettua una richiesta a un server di annunci, la risposta VAST/VMAP di solito include più creativi di annunci ( `MediaFile` elementi), ciascuno dei quali fornisce un URL a una versione diversa del codec contenitore. In alcuni casi, i creativi di annunci nella risposta VAST/VMAP forniscono ciascuno un bitrate diverso per l&#39;annuncio. Se desideri specificare la tua priorità e le regole di trasformazione per questi creativi di annunci, puoi farlo nel file di configurazione [!DNL AdobeTVSDKConfig.json] .

>[!IMPORTANT]
>
>* Non modificare il nome del file di configurazione TVSDK. Il nome deve rimanere [!DNL AdobeTVSDKConfig.json].
>* Il file deve trovarsi nella cartella [!DNL assets/] del progetto.
>* La modifica delle tracce audio durante la riproduzione dell&#39;annuncio non modifica la traccia audio. Un lettore non deve consentire agli utenti di modificare la traccia audio durante la riproduzione di un annuncio.

>



Puoi specificare due tipi di regole in [!DNL AdobeTVSDKConfig.json]: Regole *Priorità* e regole *Normalizza*.

**[!UICONTROL Ad Rules change]**

<!--<a id="section_EDCE7C94156D4A47AA2FBAE9BE0390CE"></a>-->

Le regole dell’annuncio vengono specificate utilizzando un file JSON. Il formato del file JSON rimane lo stesso in entrambe le versioni di TVSDK. Tuttavia, in TVSDK v3.0, il file JSON delle regole dell&#39;annuncio deve essere ospitato in una posizione accessibile tramite un URL HTTP. L&#39;applicazione può utilizzare un&#39;istanza di AuditudeSettings:

```
//TVSDK v3.0 AuditudeSettings result = new AuditudeSettings(); 
result.setCRSRulesJsonURL(<http url of 
AdobeTVSDKConfig.json>);  
```
