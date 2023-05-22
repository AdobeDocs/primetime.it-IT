---
description: Per il contenuto video-on-demand (VOD), TVSDK inserisce interruzioni pubblicitarie unendo gli annunci nel contenuto principale in modo che la durata della timeline aumenti.
title: Risoluzione e inserimento di annunci VOD
exl-id: c8e1423c-5d53-452c-ad01-8335ccf42471
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Risolvere e inserire annunci VOD {#resolve-and-insert-vod-ad}

Per il contenuto video-on-demand (VOD), TVSDK inserisce interruzioni pubblicitarie unendo gli annunci nel contenuto principale in modo che la durata della timeline aumenti.

Prima della riproduzione, TVSDK risolve gli annunci noti, inserisce interruzioni pubblicitarie nel contenuto principale come descritto da una timeline restituita da Adobe Primetime ad decisioning e, se necessario, ricalcola la timeline virtuale.

TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, che viene inserito prima del contenuto.
* **Mid-roll**, che si trova al centro del contenuto.
* **Post-roll**, che viene inserito dopo il contenuto.

>[!TIP]
>
>All’avvio della riproduzione, il contenuto non subirà ulteriori modifiche.

Gli annunci non possono essere:

* Inserito
* Eliminato

   Ad esempio, non puoi eliminare gli annunci incorporati dal contenuto per offrire un’esperienza senza annunci.
* Sostituito

   Ad esempio, non puoi sostituire gli annunci incorporati con annunci mirati.
