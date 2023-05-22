---
description: Sui dispositivi che supportano l'accelerazione GPU (hardware), è possibile utilizzare un oggetto flash.media.StageVideo per elaborare video sull'hardware del dispositivo. La disponibilità di StageVideo dipende dalle versioni e dalle funzionalità delle diverse parti del Flash Player, inclusi hardware video, sistema operativo, driver, browser, connessione di rete e contesto di visualizzazione.
title: Funzionalità e restrizioni di StageVideo
exl-id: 228ea2d0-5950-43f5-8cfd-640d1c482b05
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Panoramica {#stagevideo-capabilities-and-restrictions-overview}

Sui dispositivi che supportano l&#39;accelerazione GPU (hardware), è possibile utilizzare un oggetto flash.media.StageVideo per elaborare video sull&#39;hardware del dispositivo. La disponibilità di StageVideo dipende dalle versioni e dalle funzionalità delle diverse parti del Flash Player, inclusi hardware video, sistema operativo, driver, browser, connessione di rete e contesto di visualizzazione.

Il `StageVideo` questa classe consente di sfruttare l&#39;accelerazione hardware per presentare il video al livello di prestazioni più elevato possibile per un dispositivo. La disponibilità e le prestazioni di `StageVideo` è influenzato dai seguenti fattori:

* **Accelerazione hardware** - Quando è disponibile l&#39;accelerazione hardware, `StageVideo` elabora il video sull&#39;hardware del dispositivo. Quando l&#39;accelerazione hardware non è disponibile, `StageVideo` le risposte dipendono dalla versione del Flash in esecuzione:

   * *Flash 15 e versioni successive* - Quando l&#39;accelerazione hardware non è disponibile, `StageVideo` si basa sul software e non è necessario eseguire alcuna operazione.

      >[!TIP]
      >
      >Quando l&#39;accelerazione hardware non è disponibile, le prestazioni possono peggiorare in modo significativo.

   * *Flash 14 e versioni precedenti* - Quando l&#39;accelerazione hardware non è disponibile, `StageVideo` non è più disponibile. In un piccolo set di configurazioni in cui l’accelerazione hardware non è supportata dal browser o dalla GPU o è disattivata nel Flash Player, la visualizzazione video con lo stack HLS TVSDK avrà esito negativo. In *HDS* pipeline, è possibile passare da `StageVideo` a un&#39;alternativa, ad esempio l&#39;oggetto Video, che elabora il video nella CPU.

* **Contesto della presentazione** - Durante la visualizzazione a schermo intero, `StageVideo` è sempre disponibile e le prestazioni saranno al livello massimo disponibile sul dispositivo. Quando non si visualizza la presentazione a schermo intero, la presentazione video rientra nel contesto del browser, in cui vengono utilizzate le impostazioni e le funzionalità del browser.

* **wmode** - Nel contesto del browser, il `wmode` è fondamentale per le prestazioni. Adobe consiglia di mantenere `wmode` imposta su `direct` per garantire le migliori prestazioni possibili nel contesto del browser.

   >[!NOTE]
   >
   >La combinazione di fattori che includono `wmode`, `StageVideo`, e Flash determinano funzionalità e restrizioni diverse, a seconda della velocità di esecuzione dell&#39;hardware e della versione del Flash in uso.

   * *Flash 15 e versioni successive* - `StageVideo` è disponibile con tutte le opzioni `wmode` impostazioni. Tuttavia, se imposti `wmode` a un&#39;impostazione diversa da `direct`, le prestazioni risulteranno inferiori.

   * *Flash 14 e versioni precedenti* - Se si imposta `wmode` a un&#39;impostazione diversa da `direct`, `StageVideo` non è disponibile in tutti i browser.
