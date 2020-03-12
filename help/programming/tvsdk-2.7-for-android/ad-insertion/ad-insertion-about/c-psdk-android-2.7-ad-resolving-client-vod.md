---
description: Per il contenuto video-on-demand (VOD), TVSDK inserisce e interrompe le inserzioni mediante l'applicazione di una giunzione nel contenuto principale, in modo che la durata della timeline aumenti.
seo-description: Per il contenuto video-on-demand (VOD), TVSDK inserisce e interrompe le inserzioni mediante l'applicazione di una giunzione nel contenuto principale, in modo che la durata della timeline aumenti.
seo-title: Risolvere e inserire annuncio VOD
title: Risolvere e inserire annuncio VOD
uuid: 69853c16-e252-472e-b33a-7a0e0c4b95dd
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Risolvere e inserire annunci VOD {#resolve-and-insert-vod-ad}

Per il contenuto video-on-demand (VOD), TVSDK inserisce e interrompe le inserzioni mediante l&#39;applicazione di una giunzione nel contenuto principale, in modo che la durata della timeline aumenti.

Prima della riproduzione, TVSDK risolve gli annunci noti, inserisce e interrompe il contenuto principale come descritto da una timeline che viene restituita da Adobe Primetime ad Decioning e, se necessario, ricalcola la timeline virtuale.

TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, che viene posizionato prima del contenuto.
* **Media roll**, che si trova al centro del contenuto.
* **Post-roll**, che viene posizionato dopo il contenuto.

>[!TIP]
>
>Dopo l&#39;avvio della riproduzione, non è possibile apportare modifiche aggiuntive al contenuto.

Gli annunci non possono essere:

* Inserito
* Eliminato

   Ad esempio, non potete eliminare gli annunci incorporati dal contenuto per offrire un&#39;esperienza senza annunci.
* Sostituito

   Ad esempio, non potete sostituire gli annunci incorporati con annunci con targeting.

