---
description: Per poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.
seo-description: Per poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.
seo-title: Attendere uno stato valido
title: Attendere uno stato valido
uuid: 918ab021-3685-424a-b84e-683da0357724
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Attendere uno stato valido {#wait-for-a-valid-state}

Con TVSDK potete controllare l&#39;esperienza di riproduzione di base per video live e video on demand (VOD). TVSDK fornisce metodi e proprietà sull&#39;istanza del lettore che è possibile utilizzare per configurare l&#39;interfaccia utente del lettore. Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.

Il lettore passa attraverso vari stati. In attesa che il lettore sia nello stato corretto, la risorsa multimediale viene caricata correttamente. Se il lettore non ha almeno lo stato richiesto, molti metodi di lettore lanciano `IllegalStateException`.

In genere lo stato richiesto è PREPARATO.

1. Per confermare che lo stato è PREPARATO:

   Quando il lettore sta inizializzando, attendete che TVSDK chiami il callback per l&#39; `MediaPlayerStatusChangeEvent.STATUS_CHANGED` evento con stato PREPARATO.

   Verificare se lo stato corrente dell&#39; `MediaPlayer` oggetto è almeno PREPARATO.

   ```
   function getstatus():String;
   ```
