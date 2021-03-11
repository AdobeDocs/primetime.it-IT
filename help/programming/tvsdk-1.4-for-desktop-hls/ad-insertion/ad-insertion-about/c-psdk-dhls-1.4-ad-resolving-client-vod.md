---
description: Per i contenuti video-on-demand (VOD), TVSDK inserisce e interrompe unendo gli annunci nel contenuto principale in modo che la durata della timeline aumenti.
title: Risoluzione e inserimento di annunci VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Risoluzione e inserimento di annunci VOD{#vod-ad-resolving-and-insertion}

Per i contenuti video-on-demand (VOD), TVSDK inserisce e interrompe unendo gli annunci nel contenuto principale in modo che la durata della timeline aumenti.

Prima della riproduzione, TVSDK risolve gli annunci noti, inserisce e interrompe il contenuto principale come descritto da una timeline restituita da TVSDK e, se necessario, ricalcola la timeline virtuale.

TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, che è prima del contenuto.
* **Mid-roll**, che si trova nel contenuto.
* **Post-roll**, che è dopo il contenuto.

>[!IMPORTANT]
>
>Quando implementi un `AdPolicySelector` personalizzato, puoi assegnare un criterio diverso a ciascun tipo di `AdBreakTimelineItem` (pre-roll, mid-roll o post-roll) in `AdPolicyInfo`, in base al tipo di `AdBreakTimelineItem`. Ad esempio, è possibile mantenere il contenuto mid-roll dopo la riproduzione, ma rimuovere il contenuto pre-roll dopo la riproduzione.

Dopo l’avvio della riproduzione, non è possibile apportare ulteriori modifiche al contenuto. Gli annunci non possono essere:

* Inserito
* Eliminato

   Ad esempio, non puoi eliminare gli annunci incorporati dal contenuto per offrire un’esperienza senza annunci.
* Sostituito

   Ad esempio, non puoi sostituire gli annunci incorporati con annunci di destinazione.

