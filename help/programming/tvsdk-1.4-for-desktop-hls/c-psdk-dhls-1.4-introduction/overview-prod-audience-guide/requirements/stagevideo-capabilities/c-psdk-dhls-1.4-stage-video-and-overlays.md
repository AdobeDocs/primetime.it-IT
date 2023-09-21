---
description: È possibile utilizzare le sovrapposizioni HTML con StageVideo per visualizzare gli elementi dell'interfaccia utente nel piano video dell'elenco di visualizzazione del Flash. Questo piano si trova sopra il piano StageVideo, pertanto StageVideo viene sempre visualizzato dietro qualsiasi elemento dell'elenco di visualizzazione del Flash.
title: Sovrapposizioni StageVideo e HTML
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Sovrapposizioni StageVideo e HTML{#stagevideo-and-html-overlays}

È possibile utilizzare le sovrapposizioni HTML con StageVideo per visualizzare gli elementi dell&#39;interfaccia utente nel piano video dell&#39;elenco di visualizzazione del Flash. Questo piano si trova sopra il piano StageVideo, pertanto StageVideo viene sempre visualizzato dietro qualsiasi elemento dell&#39;elenco di visualizzazione del Flash.

Le sovrapposizioni HTML sono elementi dell’interfaccia utente che puoi visualizzare nel piano di visualizzazione del Flash su un video renderizzato da `StageVideo` sul proprio aereo. Prima del Flash 15, non era possibile utilizzare le sovrapposizioni HTML quando l’accelerazione hardware non era disponibile. A partire dal Flash 15, le sovrapposizioni HTML vengono visualizzate quando `StageVideo` torna al rendering software.

>[!IMPORTANT]
>
>A seconda delle funzionalità del sistema, le prestazioni possono diminuire in misura maggiore o minore quando si utilizzano le sovrapposizioni HTML.

Considera le seguenti informazioni:

* Nel Flash Player 15:

   * È possibile utilizzare le sovrapposizioni HTML se è disponibile l&#39;accelerazione hardware.
   * Per utilizzare le sovrapposizioni HTML, imposta `wmode` a `opaque`.

* Nel Flash Player 14:

   * Quando è disponibile l&#39;accelerazione hardware, `StageVideo` si trova al di sotto dell’elenco di visualizzazione del Flash, per cui puoi utilizzare le sovrapposizioni di HTML.
   * Quando l&#39;accelerazione hardware non è disponibile, il video viene riprodotto sopra tutti gli altri elementi nel browser, impedendo l&#39;utilizzo di sovrapposizioni HTML.

Di seguito sono riportati i requisiti minimi del browser per l’utilizzo delle sovrapposizioni HTML con `StageVideo`:

* Firefox versione 4 e successive
* Safari versione 4 e successive
* Internet Explorer:

   * Versione 9+ su Windows 7 e successive
   * Versione 10+ su Windows XP

* Chrome versione 26 e successive

  >[!IMPORTANT]
  >
  >Chrome Pepper su Windows XP e Windows Vista non è supportato.
