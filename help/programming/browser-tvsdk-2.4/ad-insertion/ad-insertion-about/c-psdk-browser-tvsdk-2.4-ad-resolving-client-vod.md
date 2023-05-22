---
description: Per il contenuto video-on-demand (VOD), il browser TVSDK inserisce interruzioni pubblicitarie unendo gli annunci nel contenuto principale in modo che la durata della timeline aumenti.
title: Risoluzione e inserimento di annunci VOD
exl-id: c2a2f14b-c90d-47fc-9dcc-eff8b1491dde
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Risoluzione e inserimento di annunci VOD{#vod-ad-resolving-and-insertion}

Per il contenuto video-on-demand (VOD), il browser TVSDK inserisce interruzioni pubblicitarie unendo gli annunci nel contenuto principale in modo che la durata della timeline aumenti.

Prima della riproduzione, il browser TVSDK risolve gli annunci noti, inserisce interruzioni pubblicitarie nel contenuto principale come descritto da una timeline restituita da Adobe Primetime ad decisioning e, se necessario, ricalcola la timeline virtuale.

Il browser TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, che è prima del contenuto.
* **Post-roll**, che è dopo il contenuto.

All’avvio della riproduzione, il contenuto non subirà ulteriori modifiche. Gli annunci non possono essere:

* Inserito
* Eliminato

   Ad esempio, non puoi eliminare gli annunci incorporati dal contenuto per offrire un’esperienza senza annunci.
* Sostituito

   Ad esempio, non puoi sostituire gli annunci incorporati con annunci mirati.
