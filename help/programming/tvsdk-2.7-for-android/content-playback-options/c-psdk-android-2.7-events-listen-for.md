---
description: Gli eventi di TVSDK indicano lo stato del lettore, gli errori che si verificano, il completamento delle azioni richieste, ad esempio un video che inizia a essere riprodotto o le azioni che si verificano implicitamente, ad esempio il completamento di un annuncio.
title: Ascolta gli eventi di Primetime Player
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---


# Panoramica {#listen-for-primetime-player-events-overview}

Gli eventi di TVSDK indicano lo stato del lettore, gli errori che si verificano, il completamento delle azioni richieste, ad esempio un video che inizia a essere riprodotto o le azioni che si verificano implicitamente, ad esempio il completamento di un annuncio.

Poiché l’applicazione deve rispondere a molti di questi eventi, è necessario implementare le routine di gestione degli eventi e registrare tali routine con TVSDK. Le routine chiamano i metodi TVSDK pertinenti per rispondere in modo appropriato.

Ulteriori informazioni sugli eventi:

* La natura in tempo reale della riproduzione video richiede un’attività asincrona (non di blocco) per molte operazioni TVSDK.
* TVSDK supporta un lettore video basato su eventi.

   Fornisce eventi che corrispondono a tutti i passaggi importanti del processo di gioco. Puoi registrare tali eventi con il meccanismo eventi della piattaforma e creare gestori eventi che verranno chiamati quando si verificano tali eventi. *`Event Handlers`* sono noti anche come routine di callback o listener di eventi. TVSDK fornisce una gamma completa di metodi che possono essere utilizzati dai gestori eventi.
* In genere, l’applicazione avvia operazioni non di blocco, ad esempio per richiedere l’avvio della riproduzione di un video.

   TVSDK comunica in modo asincrono con l’applicazione inviando eventi, ad esempio quando il video inizia la riproduzione e un evento al termine del video. Altri eventi possono indicare cambiamenti di stato nel lettore e condizioni di errore. I gestori eventi eseguono le azioni appropriate.