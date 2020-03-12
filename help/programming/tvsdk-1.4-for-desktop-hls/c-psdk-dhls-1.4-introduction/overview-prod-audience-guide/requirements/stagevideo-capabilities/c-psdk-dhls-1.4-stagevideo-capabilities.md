---
description: Sui dispositivi che supportano l'accelerazione GPU (hardware), potete utilizzare un oggetto flash.media.StageVideo per elaborare video sull'hardware del dispositivo. La disponibilità di StageVideo dipende dalle versioni e capacità di diverse parti del sistema, tra cui Flash Player, hardware video, SO, driver, browser, connessione di rete e contesto di visualizzazione.
seo-description: Sui dispositivi che supportano l'accelerazione GPU (hardware), potete utilizzare un oggetto flash.media.StageVideo per elaborare video sull'hardware del dispositivo. La disponibilità di StageVideo dipende dalle versioni e capacità di diverse parti del sistema, tra cui Flash Player, hardware video, SO, driver, browser, connessione di rete e contesto di visualizzazione.
seo-title: Funzioni e limitazioni di StageVideo
title: Funzioni e limitazioni di StageVideo
uuid: 7556f30b-4b9f-4258-beb6-2a4ce8f05d1a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Panoramica {#stagevideo-capabilities-and-restrictions-overview}

Sui dispositivi che supportano l&#39;accelerazione GPU (hardware), potete utilizzare un oggetto flash.media.StageVideo per elaborare video sull&#39;hardware del dispositivo. La disponibilità di StageVideo dipende dalle versioni e capacità di diverse parti del sistema, tra cui Flash Player, hardware video, SO, driver, browser, connessione di rete e contesto di visualizzazione.

Questa `StageVideo` classe consente di sfruttare l&#39;accelerazione hardware per presentare video al livello di prestazioni più elevato possibile per un dispositivo. La disponibilità e le prestazioni di `StageVideo` è influenzata dai seguenti fattori:

* **Accelerazione** hardware: quando è disponibile l&#39;accelerazione hardware, `StageVideo` elabora il video sull&#39;hardware del dispositivo. Quando l’accelerazione hardware non è disponibile, la `StageVideo` risposta dipende dalla versione di Flash in esecuzione:

   * *Flash 15 e versioni successive* : quando l&#39;accelerazione hardware non è disponibile, `StageVideo` si ripete al software e non è necessario eseguire alcuna operazione.

      >[!TIP]
      >
      >Se l&#39;accelerazione hardware non è disponibile, le prestazioni possono diminuire in modo significativo.

   * *Flash 14 e versioni precedenti* : quando l&#39;accelerazione hardware non è disponibile, `StageVideo` diventa non disponibile. In un piccolo set di configurazioni in cui l’accelerazione hardware non è supportata dal browser o dalla GPU o è disattivata in Flash Player, la visualizzazione video con lo stack TVSDK HLS avrà esito negativo. Nella pipeline *HDS* , potete passare da `StageVideo` a un&#39;alternativa, come l&#39;oggetto Video, che elabora il video nella CPU.

* **Contesto** della presentazione - Durante la visualizzazione a schermo intero, `StageVideo` è sempre disponibile e le prestazioni saranno al livello massimo disponibile sul dispositivo. Quando non viene visualizzata a schermo intero, la presentazione video rientra nel contesto del browser, dove vengono utilizzate le impostazioni e le funzionalità del browser.

* **wmode** - Nel contesto del browser, l&#39; `wmode` impostazione è fondamentale per le prestazioni. Adobe consiglia di mantenere `wmode` impostato `direct` in modo da garantire le migliori prestazioni possibili nel contesto del browser.

   >[!NOTE]
   >
   >La combinazione di fattori che includono `wmode`, `StageVideo`e Flash comporta capacità e restrizioni diverse, a seconda della velocità di esecuzione dell’hardware e della versione di Flash in uso.

   * *Flash 15 e versioni successive* - `StageVideo` è disponibile con tutte le `wmode` impostazioni disponibili. Tuttavia, se impostate `wmode` un&#39;impostazione diversa da `direct`, le prestazioni risulteranno inferiori.

   * *Flash 14 e versioni precedenti* - Se si imposta `wmode` un&#39;impostazione diversa da `direct`, non `StageVideo` è disponibile in tutti i browser.

