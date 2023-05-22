---
description: Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve trovarsi in uno stato valido.
title: Attesa di uno stato valido
exl-id: a225688a-e272-441d-90d2-5ee2c259ca9d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Attesa di uno stato valido {#wait-for-a-valid-state}

Con TVSDK è possibile controllare l’esperienza di riproduzione di base per live e video on-demand (VOD). TVSDK fornisce metodi e proprietà sull&#39;istanza del lettore che è possibile utilizzare per configurare l&#39;interfaccia utente del lettore. Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve trovarsi in uno stato valido.

Il lettore si sposta attraverso vari stati. L’attesa che il lettore sia nello stato corretto assicura che la risorsa multimediale sia stata caricata correttamente. Se il lettore non è nello stato richiesto, vengono lanciati molti metodi del lettore `IllegalStateException`.

Lo stato richiesto è in genere PREPARATO.

1. Per confermare che lo stato è PREPARATO:

   Quando il lettore viene inizializzato, attendi che TVSDK chiami il callback per `MediaPlayerStatusChangeEvent.STATUS_CHANGED` evento con stato PREPARATO.

   Per verificare se lo stato corrente del `MediaPlayer` l&#39;oggetto è almeno PREPARATO.

   ```
   function getstatus():String;
   ```
