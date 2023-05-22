---
description: Con TVSDK è possibile controllare l’esperienza di riproduzione di base per live e video on-demand (VOD). TVSDK fornisce metodi e proprietà sull’istanza del lettore che è possibile utilizzare per configurare l’interfaccia utente del lettore.
title: Attesa di uno stato valido
exl-id: ab9da066-429f-44ca-b2e7-2bde9e5c0f90
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Attesa di uno stato valido {#wait-for-a-valid-state}

Con TVSDK è possibile controllare l’esperienza di riproduzione di base per live e video on-demand (VOD). TVSDK fornisce metodi e proprietà sull’istanza del lettore che è possibile utilizzare per configurare l’interfaccia utente del lettore.

Prima di poter utilizzare la maggior parte dei metodi del lettore TVSDK, il lettore deve trovarsi in uno stato valido.
Il lettore si sposta attraverso vari stati. L’attesa che il lettore si trovi nello stato corretto assicura che la risorsa multimediale sia stata caricata correttamente. Se il lettore non si trova almeno nello stato richiesto, vengono lanciati molti metodi del lettore `IllegalStateException`.

Lo stato richiesto è in genere PREPARATO.
