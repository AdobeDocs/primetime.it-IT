---
description: Gli eventi dal TVSDK del browser indicano lo stato del lettore, gli errori che si verificano, il completamento delle azioni richieste, ad esempio l’avvio della riproduzione di un video, o le azioni che si verificano implicitamente, ad esempio il completamento di un annuncio.
title: Ascolta gli eventi di Primetime Player
exl-id: e16fa356-5286-4cae-b7ce-74a2e8093d62
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%

---

# Panoramica {#listen-for-primetime-player-events-overview}

Gli eventi dal TVSDK del browser indicano lo stato del lettore, gli errori che si verificano, il completamento delle azioni richieste, ad esempio l’avvio della riproduzione di un video, o le azioni che si verificano implicitamente, ad esempio il completamento di un annuncio.

Poiché l&#39;applicazione deve rispondere a molti di questi eventi, è necessario implementare routine di gestione degli eventi e registrare tali routine con il TVSDK del browser. Le routine chiamano i metodi TVSDK del browser pertinenti per rispondere in modo appropriato.

Seguono alcune informazioni aggiuntive sugli eventi:

* La natura in tempo reale della riproduzione video richiede un’attività asincrona (non bloccante) per molte operazioni TVSDK del browser.
* Il browser TVSDK supporta un lettore video basato su eventi.

   Fornisce eventi che corrispondono a tutti i passaggi importanti nel processo di riproduzione. Registra tali eventi con il meccanismo degli eventi della piattaforma e crea gestori di eventi che verranno chiamati quando si verificano tali eventi. *`Event Handlers`* sono anche note come routine di callback o listener di eventi. Browser TVSDK fornisce una gamma completa di metodi che possono essere utilizzati dai gestori di eventi.
* L’applicazione in genere avvia operazioni non di blocco, ad esempio la richiesta che venga avviata la riproduzione di un video.

   Il browser TVSDK comunica in modo asincrono con l’applicazione inviando eventi, come ad esempio quando inizia la riproduzione del video e un evento al termine del video. Altri eventi possono indicare modifiche di stato nel lettore e condizioni di errore. I gestori eventi eseguono le azioni appropriate.
