---
description: Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.
title: Attendi uno stato valido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Attendi uno stato valido {#wait-for-a-valid-state}

Con TVSDK è possibile controllare l&#39;esperienza di riproduzione di base per live e video on demand (VOD). TVSDK fornisce metodi e proprietà sull&#39;istanza del lettore che è possibile utilizzare per configurare l&#39;interfaccia utente del lettore. Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve avere uno stato valido.

Il lettore passa attraverso vari stati. In attesa che il lettore sia nello stato corretto, la risorsa multimediale viene caricata correttamente. Se il lettore non è almeno nello stato richiesto, molti metodi del lettore lanciano `IllegalStateException`.

In genere lo stato richiesto è PREPARATO.

1. Per confermare che lo stato è PREPARATO:

   Quando il lettore sta inizializzando, attendi che TVSDK chiami il callback per l&#39;evento `MediaPlayerStatusChangeEvent.STATUS_CHANGED` con stato PREPARED.

   Verificare se lo stato corrente dell&#39;oggetto `MediaPlayer` è almeno PREPARATO.

   ```
   function getstatus():String;
   ```
