---
description: Sui dispositivi che supportano l'accelerazione GPU (hardware), è possibile utilizzare un oggetto flash.media.StageVideo per elaborare video sull'hardware del dispositivo. La disponibilità di StageVideo dipende dalle versioni e capacità di diverse parti del sistema, tra cui Flash Player, hardware video, sistema operativo, driver, browser, connessione di rete e contesto di visualizzazione.
title: Funzionalità e limitazioni di StageVideo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Panoramica {#stagevideo-capabilities-and-restrictions-overview}

Sui dispositivi che supportano l&#39;accelerazione GPU (hardware), è possibile utilizzare un oggetto flash.media.StageVideo per elaborare video sull&#39;hardware del dispositivo. La disponibilità di StageVideo dipende dalle versioni e capacità di diverse parti del sistema, tra cui Flash Player, hardware video, sistema operativo, driver, browser, connessione di rete e contesto di visualizzazione.

La classe `StageVideo` consente di sfruttare l&#39;accelerazione hardware per presentare video al livello di prestazioni più elevato possibile per un dispositivo. La disponibilità e le prestazioni di `StageVideo` sono influenzate dai seguenti fattori:

* **Accelerazione hardware**  - Quando l&#39;accelerazione hardware è disponibile,  `StageVideo` elabora i video sull&#39;hardware del dispositivo. Quando l&#39;accelerazione hardware non è disponibile, la risposta `StageVideo` dipende dalla versione del Flash in esecuzione:

   * *Flash 15 e versioni successive*  - Quando l&#39;accelerazione hardware non è disponibile,  `StageVideo` torna al software e non è necessario eseguire alcuna operazione.

      >[!TIP]
      >
      >Quando l&#39;accelerazione hardware non è disponibile, le prestazioni possono degradarsi in modo significativo.

   * *Flash 14 e versioni precedenti*  - Quando l&#39;accelerazione hardware non è disponibile,  `StageVideo` diventa non disponibile. In un piccolo set di configurazioni in cui l’accelerazione hardware non è supportata dal browser o dalla GPU o è disattivata nel Flash Player, la visualizzazione video con lo stack TVSDK HLS avrà esito negativo. Nella pipeline *HDS* puoi passare da `StageVideo` a un&#39;alternativa, come l&#39;oggetto Video, che elabora il video nella CPU.

* **Contesto della presentazione**  - Durante la visualizzazione a schermo intero,  `StageVideo` è sempre disponibile e le prestazioni saranno al livello massimo disponibile sul dispositivo. Quando non visualizzi a schermo intero, la presentazione video rientra nel contesto del browser, in cui vengono utilizzate le impostazioni e le funzionalità del browser.

* **wmode**  - Nel contesto del browser, l&#39; `wmode` impostazione è fondamentale per le prestazioni. L’Adobe consiglia di mantenere `wmode` impostato su `direct` per garantire le migliori prestazioni possibili nel contesto del browser.

   >[!NOTE]
   >
   >La combinazione di fattori che includono `wmode`, `StageVideo` e il Flash determina funzionalità e restrizioni diverse, a seconda della velocità di esecuzione dell&#39;hardware e della versione del Flash in uso.

   * *Flash 15 e versioni successive*  -  `StageVideo` è disponibile con tutte le  `wmode` impostazioni disponibili. Tuttavia, se si imposta `wmode` su un&#39;impostazione diversa da `direct`, le prestazioni saranno inferiori.

   * *Flash 14 e versioni precedenti* : se imposti  `wmode` su un’impostazione diversa da  `direct`, non  `StageVideo` è disponibile in tutti i browser.

