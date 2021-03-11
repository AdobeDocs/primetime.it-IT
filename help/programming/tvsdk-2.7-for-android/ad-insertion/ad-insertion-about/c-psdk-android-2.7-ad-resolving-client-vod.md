---
description: Per i contenuti video-on-demand (VOD), TVSDK inserisce e interrompe unendo gli annunci nel contenuto principale in modo che la durata della timeline aumenti.
title: Risolvi e inserisci annuncio VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Risolvere e inserire annunci VOD {#resolve-and-insert-vod-ad}

Per i contenuti video-on-demand (VOD), TVSDK inserisce e interrompe unendo gli annunci nel contenuto principale in modo che la durata della timeline aumenti.

Prima della riproduzione, TVSDK risolve gli annunci noti, inserisce e interrompe il contenuto principale come descritto da una timeline che viene restituita da Adobe Primetime ad Decioning e, se necessario, ricalcola la timeline virtuale.

TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, che viene posizionato prima del contenuto.
* **Mid-roll**, che si trova al centro del contenuto.
* **Post-roll**, che viene posizionato dopo il contenuto.

>[!TIP]
>
>Dopo l’avvio della riproduzione, non è possibile apportare ulteriori modifiche al contenuto.

Gli annunci non possono essere:

* Inserito
* Eliminato

   Ad esempio, non puoi eliminare gli annunci incorporati dal contenuto per offrire un’esperienza senza annunci.
* Sostituito

   Ad esempio, non puoi sostituire gli annunci incorporati con annunci di destinazione.

