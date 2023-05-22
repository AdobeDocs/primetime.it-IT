---
description: Per il contenuto video-on-demand (VOD), TVSDK inserisce interruzioni pubblicitarie unendo gli annunci nel contenuto principale in modo che la durata della timeline aumenti.
title: Risoluzione e inserimento di annunci VOD
exl-id: 6f02c7fc-028d-442f-92d4-9efa671b7f02
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Risoluzione e inserimento di annunci VOD{#vod-ad-resolving-and-insertion}

Per il contenuto video-on-demand (VOD), TVSDK inserisce interruzioni pubblicitarie unendo gli annunci nel contenuto principale in modo che la durata della timeline aumenti.

Prima della riproduzione, TVSDK risolve gli annunci noti, inserisce interruzioni pubblicitarie nel contenuto principale come descritto da una timeline restituita da TVSDK e, se necessario, ricalcola la timeline virtuale.

TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, che è prima del contenuto.
* **Mid-roll**, che si trova nel contenuto.
* **Post-roll**, che è dopo il contenuto.

>[!IMPORTANT]
>
>Quando si implementa una `AdPolicySelector`, è possibile assegnare un criterio diverso a ogni tipo di `AdBreakTimelineItem` (pre-roll, mid-roll o post-roll) in `AdPolicyInfo`, in base al tipo di `AdBreakTimelineItem`. Ad esempio, puoi mantenere il contenuto mid-roll dopo la riproduzione, ma rimuoverlo dopo la riproduzione.

All’avvio della riproduzione, il contenuto non subirà ulteriori modifiche. Gli annunci non possono essere:

* Inserito
* Eliminato

   Ad esempio, non puoi eliminare gli annunci incorporati dal contenuto per offrire un’esperienza senza annunci.
* Sostituito

   Ad esempio, non puoi sostituire gli annunci incorporati con annunci mirati.
