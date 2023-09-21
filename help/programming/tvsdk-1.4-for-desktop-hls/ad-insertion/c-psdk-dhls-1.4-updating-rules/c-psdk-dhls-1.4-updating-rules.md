---
description: Puoi utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione degli annunci creativi nelle risposte VAST/VMAP. Puoi anche utilizzare questo file di configurazione per definire le regole di trasformazione dell’URL di origine per le creatività dell’annuncio.
title: Aggiornamento delle regole di selezione creativa degli annunci
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Panoramica {#updating-ad-creative-selection-rules}

Puoi utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione degli annunci creativi nelle risposte VAST/VMAP. Puoi anche utilizzare questo file di configurazione per definire le regole di trasformazione dell’URL di origine per le creatività dell’annuncio.

Quando il lettore video effettua una richiesta a un ad server, la risposta VAST/VMAP di solito include più creativi di annunci ( `MediaFile` elementi ), ciascuno dei quali fornisce un URL per una versione diversa del codec contenitore. In alcuni casi, i creativi degli annunci nella risposta VAST/VMAP forniscono ciascuno un bitrate diverso per l’annuncio. Se desideri specificare la tua priorità e le regole di trasformazione per queste creatività di annunci, puoi farlo in [!DNL AdobeTVSDKConfig.json] file di configurazione.

>[!IMPORTANT]
>
>* Non modificare il nome del file di configurazione TVSDK. Il nome deve rimanere [!DNL AdobeTVSDKConfig.json].
>* Questo file deve essere ospitato sulla rete CDN (Content Delivery Network).
>

È possibile specificare due tipi di regole in [!DNL AdobeTVSDKConfig.json]: *Priorità* regole e *Normalizza* regole.
