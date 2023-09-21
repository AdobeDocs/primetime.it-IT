---
description: Per il contenuto video-on-demand (VOD), il browser TVSDK inserisce interruzioni pubblicitarie unendo gli annunci nel contenuto principale in modo che la durata della timeline aumenti.
title: Risoluzione e inserimento di annunci VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
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
