---
description: Gli eventi di TVSDK indicano lo stato del lettore, gli errori che si verificano, il completamento delle azioni richieste, come un video che inizia a essere riprodotto o le azioni che si verificano implicitamente, come un annuncio che completa.
seo-description: Gli eventi di TVSDK indicano lo stato del lettore, gli errori che si verificano, il completamento delle azioni richieste, come un video che inizia a essere riprodotto o le azioni che si verificano implicitamente, come un annuncio che completa.
seo-title: Ascoltare gli eventi di Primetime Player
title: Ascoltare gli eventi di Primetime Player
uuid: 3aa0979c-6141-4098-9f19-d5fe23192827
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Panoramica {#listen-for-primetime-player-events-overview}

Gli eventi di TVSDK indicano lo stato del lettore, gli errori che si verificano, il completamento delle azioni richieste, come un video che inizia a essere riprodotto o le azioni che si verificano implicitamente, come un annuncio che completa.

Poiché l’applicazione deve rispondere a molti di questi eventi, è necessario implementare le routine di gestione degli eventi e registrare tali routine con TVSDK. Le routine chiamano i metodi TVSDK pertinenti per rispondere in modo appropriato.

Ulteriori informazioni sugli eventi:

* La natura in tempo reale della riproduzione video richiede un&#39;attività asincrona (non blocco) per molte operazioni TVSDK.
* TVSDK supporta un lettore video basato su eventi.

   Fornisce eventi che corrispondono a tutti i passaggi importanti del processo di riproduzione. Potete registrare tali eventi con il meccanismo evento della piattaforma e creare gestori di eventi che verranno chiamati al verificarsi di tali eventi. *`Event Handlers`* sono noti anche come routine di callback o listener di eventi. TVSDK fornisce una gamma completa di metodi che possono essere utilizzati dai gestori eventi.
* In genere, l’applicazione avvia operazioni di non blocco, ad esempio la richiesta di avviare la riproduzione di un video.

   TVSDK comunica in modo asincrono con l&#39;applicazione inviando eventi, ad esempio all&#39;avvio della riproduzione del video e un evento al termine del video. Altri eventi possono indicare cambiamenti di stato nel lettore e condizioni di errore. I gestori dell&#39;evento eseguono le azioni appropriate.