---
description: Puoi utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione creativa degli annunci sulle risposte VAST/VMAP. Puoi anche utilizzare questo file di configurazione per definire le regole di trasformazione dell’URL di origine per gli inserzionisti.
title: Aggiornamento delle regole di selezione pubblicitaria
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# Panoramica {#updating-ad-creative-selection-rules}

Puoi utilizzare il file di configurazione TVSDK (AdobeTVSDKConfig.json) per aggiornare le priorità per la selezione creativa degli annunci sulle risposte VAST/VMAP. Puoi anche utilizzare questo file di configurazione per definire le regole di trasformazione dell’URL di origine per gli inserzionisti.

Quando il lettore video effettua una richiesta a un server di annunci, la risposta VAST/VMAP di solito include più creativi di annunci ( `MediaFile` elementi), ciascuno dei quali fornisce un URL a una versione diversa del codec contenitore. In alcuni casi, i creativi di annunci nella risposta VAST/VMAP forniscono ciascuno un bitrate diverso per l&#39;annuncio. Se desideri specificare la tua priorità e le regole di trasformazione per questi creativi di annunci, puoi farlo nel file di configurazione [!DNL AdobeTVSDKConfig.json] .

>[!IMPORTANT]
>
>* Non modificare il nome del file di configurazione TVSDK. Il nome deve rimanere [!DNL AdobeTVSDKConfig.json].
>* Questo file deve essere ospitato sulla rete CDN (Content Delivery Network).

>



Puoi specificare due tipi di regole in [!DNL AdobeTVSDKConfig.json]: Regole *Priorità* e regole *Normalizza*.
