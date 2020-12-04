---
description: Per i contenuti video su richiesta (VOD), Browser TVSDK inserisce e interrompe le inserzioni pubblicitarie nel contenuto principale in modo che la durata della timeline aumenti.
seo-description: Per i contenuti video su richiesta (VOD), Browser TVSDK inserisce e interrompe le inserzioni pubblicitarie nel contenuto principale in modo che la durata della timeline aumenti.
seo-title: VOD e risoluzione e inserimento
title: VOD e risoluzione e inserimento
uuid: 34a30ae5-d553-4c5d-9829-8e5eaa41c104
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Risoluzione e inserimento di annunci VOD{#vod-ad-resolving-and-insertion}

Per i contenuti video su richiesta (VOD), Browser TVSDK inserisce e interrompe le inserzioni pubblicitarie nel contenuto principale in modo che la durata della timeline aumenti.

Prima della riproduzione, Browser TVSDK risolve gli annunci noti, inserisce ed interrompe il contenuto principale come descritto da una timeline che viene restituita da  Adobe Primetime ad Decisionioning e, se necessario, ricalcola la timeline virtuale.

Il browser TVSDK inserisce gli annunci nei seguenti modi:

* **Pre-roll**, ovvero prima del contenuto.
* **Post-roll**, ovvero dopo il contenuto.

Dopo l&#39;avvio della riproduzione, non è possibile apportare modifiche aggiuntive al contenuto. Gli annunci non possono essere:

* Inserito
* Eliminato

   Ad esempio, non potete eliminare gli annunci incorporati dal contenuto per offrire un&#39;esperienza senza annunci.
* Sostituito

   Ad esempio, non potete sostituire gli annunci incorporati con annunci con targeting.

