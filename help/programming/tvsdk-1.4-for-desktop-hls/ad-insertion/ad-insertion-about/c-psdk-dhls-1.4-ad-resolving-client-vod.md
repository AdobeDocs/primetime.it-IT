---
description: Per il contenuto video-on-demand (VOD), TVSDK inserisce e interrompe le inserzioni mediante l'applicazione di una giunzione nel contenuto principale, in modo che la durata della timeline aumenti.
seo-description: Per il contenuto video-on-demand (VOD), TVSDK inserisce e interrompe le inserzioni mediante l'applicazione di una giunzione nel contenuto principale, in modo che la durata della timeline aumenti.
seo-title: VOD e risoluzione e inserimento
title: VOD e risoluzione e inserimento
uuid: c1017483-5b4f-4d71-9589-fb2327b4572b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# VOD e risoluzione e inserimento{#vod-ad-resolving-and-insertion}

Per il contenuto video-on-demand (VOD), TVSDK inserisce e interrompe le inserzioni mediante l&#39;applicazione di una giunzione nel contenuto principale, in modo che la durata della timeline aumenti.

Prima della riproduzione, TVSDK risolve gli annunci noti, inserisce e interrompe il contenuto principale come descritto da una timeline che viene restituita da TVSDK e, se necessario, ricalcola la timeline virtuale.

TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, ovvero prima del contenuto.
* **Mid-roll**, contenuto.
* **Post-roll**, ovvero dopo il contenuto.

>[!IMPORTANT]
>
>Durante l&#39;implementazione di un&#39;applicazione personalizzata `AdPolicySelector`, è possibile assegnare un criterio diverso a ciascun tipo di `AdBreakTimelineItem` (preroll, rollio medio o post-roll) in `AdPolicyInfo`, in base al tipo di `AdBreakTimelineItem`. Ad esempio, potete mantenere il contenuto mid-roll dopo che è stato riprodotto ma rimuovere il contenuto pre-roll dopo che è stato riprodotto.

Dopo l&#39;avvio della riproduzione, non è possibile apportare modifiche aggiuntive al contenuto. Gli annunci non possono essere:

* Inserito
* Eliminato

   Ad esempio, non potete eliminare gli annunci incorporati dal contenuto per offrire un&#39;esperienza senza annunci.
* Sostituito

   Ad esempio, non potete sostituire gli annunci incorporati con annunci con targeting.

