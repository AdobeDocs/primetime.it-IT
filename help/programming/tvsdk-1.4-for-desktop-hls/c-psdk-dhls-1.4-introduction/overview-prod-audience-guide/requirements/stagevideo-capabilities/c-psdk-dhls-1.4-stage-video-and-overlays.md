---
description: Potete utilizzare le sovrapposizioni HTML con StageVideo per visualizzare gli elementi dell'interfaccia utente nel piano video dell'elenco di visualizzazione Flash. Questo piano si trova sopra il piano StageVideo, quindi StageVideo viene sempre visualizzato dietro qualsiasi elemento dell'elenco di visualizzazione Flash.
seo-description: Potete utilizzare le sovrapposizioni HTML con StageVideo per visualizzare gli elementi dell'interfaccia utente nel piano video dell'elenco di visualizzazione Flash. Questo piano si trova sopra il piano StageVideo, quindi StageVideo viene sempre visualizzato dietro qualsiasi elemento dell'elenco di visualizzazione Flash.
seo-title: Sovrapposizioni StageVideo e HTML
title: Sovrapposizioni StageVideo e HTML
uuid: 84e862ab-4c35-47a2-9c4e-f792d3ef5363
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Sovrapposizioni StageVideo e HTML{#stagevideo-and-html-overlays}

Potete utilizzare le sovrapposizioni HTML con StageVideo per visualizzare gli elementi dell&#39;interfaccia utente nel piano video dell&#39;elenco di visualizzazione Flash. Questo piano si trova sopra il piano StageVideo, quindi StageVideo viene sempre visualizzato dietro qualsiasi elemento dell&#39;elenco di visualizzazione Flash.

Le sovrapposizioni HTML sono elementi dell&#39;interfaccia utente che potete visualizzare nel piano di visualizzazione Flash su un video rappresentato da un `StageVideo` piano specifico. Prima di Flash 15, non era possibile utilizzare sovrapposizioni HTML quando l&#39;accelerazione hardware non era disponibile. A partire da Flash 15, le sovrapposizioni HTML vengono visualizzate quando `StageVideo` torna al rendering del software.

>[!IMPORTANT]
>
>A seconda delle capacità del sistema, le prestazioni possono diminuire in misura maggiore o minore quando si utilizzano le sovrapposizioni HTML.

Considerate le seguenti informazioni:

* In Flash Player 15:

   * Potete utilizzare le sovrapposizioni HTML se l&#39;accelerazione hardware è disponibile.
   * Per utilizzare le sovrapposizioni HTML, impostate `wmode` su `opaque`.

* In Flash Player 14:

   * Quando l&#39;accelerazione hardware è disponibile, `StageVideo` si trova sotto l&#39;elenco di visualizzazione Flash, in modo da poter utilizzare le sovrapposizioni HTML.
   * Se l’accelerazione hardware non è disponibile, il video viene rappresentato sopra a tutti gli altri elementi del browser, il che impedisce l’utilizzo di sovrapposizioni HTML.

Di seguito sono riportati i requisiti minimi del browser per utilizzare le sovrapposizioni HTML con `StageVideo`:

* Firefox versione 4 e successive
* Safari versione 4 e successive
* Internet Explorer:

   * Versione 9+ in Windows 7 e versioni successive
   * Versione 10+ in Windows XP

* Chrome versione 26 e successive

   >[!IMPORTANT]
   >
   >Chrome Pepper in Windows XP e Windows Vista non è supportato.

