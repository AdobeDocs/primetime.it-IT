---
description: Potete utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione di annunci creativi sulle risposte VAST/VMAP. Potete anche utilizzare questo file di configurazione per definire le regole di trasformazione dell'URL di origine per gli annunci creativi.
seo-description: Potete utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione di annunci creativi sulle risposte VAST/VMAP. Potete anche utilizzare questo file di configurazione per definire le regole di trasformazione dell'URL di origine per gli annunci creativi.
seo-title: Aggiornamento delle regole di selezione di annunci pubblicitari
title: Aggiornamento delle regole di selezione di annunci pubblicitari
uuid: 9eb4ccc2-425f-4c01-a095-f2043df4e25c
translation-type: tm+mt
source-git-commit: 6837c753b2f031b024ff510cda670340f346c4e1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%

---


# Panoramica {#updating-ad-creative-selection-rules}

Potete utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione di annunci creativi sulle risposte VAST/VMAP. Potete anche utilizzare questo file di configurazione per definire le regole di trasformazione dell&#39;URL di origine per gli annunci creativi.

Quando il lettore video effettua una richiesta a un server di annunci, la risposta VAST/VMAP in genere include più creativi ( `MediaFile` elementi), ciascuno dei quali fornisce un URL a una versione diversa del codec contenitore. In alcuni casi, gli annunci pubblicitari creativi nella risposta VAST/VMAP forniscono per ciascuno un bitrate diverso. Se desiderate specificare la vostra priorità e le regole di trasformazione per queste creative pubblicitarie, potete farlo nel file di configurazione [!DNL AdobeTVSDKConfig.json].

>[!IMPORTANT]
>
>* Non modificate il nome del file di configurazione TVSDK. Il nome deve rimanere [!DNL AdobeTVSDKConfig.json].
>* Questo file deve essere in hosting sulla rete di distribuzione dei contenuti (CDN).

>



È possibile specificare due tipi di regole in [!DNL AdobeTVSDKConfig.json]: Regole *Priority* e *Normalize*.
