---
description: È possibile utilizzare le sovrapposizioni HTML con StageVideo per visualizzare gli elementi dell’interfaccia utente nel piano video dell’elenco di visualizzazione del Flash. Questo piano si trova sopra il piano StageVideo, quindi StageVideo viene sempre visualizzato dietro qualsiasi elemento elenco di visualizzazione Flash.
title: Sovrapposizioni StageVideo e HTML
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# Sovrapposizioni StageVideo e HTML{#stagevideo-and-html-overlays}

È possibile utilizzare le sovrapposizioni HTML con StageVideo per visualizzare gli elementi dell’interfaccia utente nel piano video dell’elenco di visualizzazione del Flash. Questo piano si trova sopra il piano StageVideo, quindi StageVideo viene sempre visualizzato dietro qualsiasi elemento elenco di visualizzazione Flash.

Le sovrapposizioni HTML sono elementi dell’interfaccia utente che possono essere visualizzati nel piano di visualizzazione del Flash su un video di cui è eseguito il rendering da `StageVideo` sul proprio piano. Prima del Flash 15, non era possibile utilizzare sovrapposizioni HTML quando l&#39;accelerazione hardware non era disponibile. A partire dal Flash 15, le sovrapposizioni HTML vengono visualizzate quando `StageVideo` torna al rendering del software.

>[!IMPORTANT]
>
>A seconda delle funzionalità del sistema, le prestazioni possono peggiorare di più o meno quando si utilizzano sovrapposizioni HTML.

Considera le seguenti informazioni:

* al Flash Player 15:

   * È possibile utilizzare le sovrapposizioni HTML se l&#39;accelerazione hardware è disponibile.
   * Per utilizzare le sovrapposizioni HTML, imposta `wmode` su `opaque`.

* al Flash Player 14:

   * Quando l&#39;accelerazione hardware è disponibile, `StageVideo` si trova sotto l&#39;elenco di visualizzazione del Flash, in modo da poter utilizzare le sovrapposizioni HTML.
   * Quando l’accelerazione hardware non è disponibile, il video viene riprodotto sopra tutti gli altri elementi del browser, impedendo l’utilizzo di sovrapposizioni HTML.

Di seguito sono riportati i requisiti minimi del browser per utilizzare le sovrapposizioni HTML con `StageVideo`:

* Firefox versione 4 e successive
* Safari versione 4 e successive
* Internet Explorer:

   * Versione 9+ su Windows 7 e versioni successive
   * Versione 10+ in Windows XP

* Chrome versione 26 e successive

   >[!IMPORTANT]
   >
   >Il peperoncino Chrome su Windows XP e Windows Vista non è supportato.

