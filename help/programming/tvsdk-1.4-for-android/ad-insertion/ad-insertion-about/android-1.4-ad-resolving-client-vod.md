---
description: Per il contenuto video-on-demand (VOD), TVSDK inserisce e interrompe le inserzioni mediante l'applicazione di una giunzione nel contenuto principale, in modo che la durata della timeline aumenti.
seo-description: Per il contenuto video-on-demand (VOD), TVSDK inserisce e interrompe le inserzioni mediante l'applicazione di una giunzione nel contenuto principale, in modo che la durata della timeline aumenti.
seo-title: VOD e risoluzione e inserimento
title: VOD e risoluzione e inserimento
uuid: 33280792-ad08-41c1-b180-cc2159e8137c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Risoluzione e inserimento di annunci VOD{#vod-ad-resolving-and-insertion}

Per il contenuto video-on-demand (VOD), TVSDK inserisce e interrompe le inserzioni mediante l&#39;applicazione di una giunzione nel contenuto principale, in modo che la durata della timeline aumenti.

Prima della riproduzione, TVSDK risolve gli annunci noti, inserisce e interrompe il contenuto principale come descritto da una timeline che viene restituita da  Adobe Primetime ad Decisionioning e, se necessario, ricalcola la timeline virtuale.

TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, ovvero prima del contenuto.
* **Mid-roll**, contenuto.
* **Post-roll**, ovvero dopo il contenuto.

Dopo l&#39;avvio della riproduzione, non è possibile apportare modifiche aggiuntive al contenuto. Gli annunci non possono essere:

* Inserito
* Eliminato

   Ad esempio, non potete eliminare gli annunci incorporati dal contenuto per offrire un&#39;esperienza senza annunci.
* Sostituito

   Ad esempio, non potete sostituire gli annunci incorporati con annunci con targeting.

