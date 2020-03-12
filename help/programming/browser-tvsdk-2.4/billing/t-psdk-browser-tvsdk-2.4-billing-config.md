---
description: Se utilizzi la configurazione predefinita, non è necessario fare altro per abilitare o configurare la fatturazione. Se avete ottenuto diversi parametri di configurazione dal rappresentante Adobe Enablement, utilizzate la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.
seo-description: Se utilizzi la configurazione predefinita, non è necessario fare altro per abilitare o configurare la fatturazione. Se avete ottenuto diversi parametri di configurazione dal rappresentante Adobe Enablement, utilizzate la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.
seo-title: Configurare le metriche di fatturazione
title: Configurare le metriche di fatturazione
uuid: 04d3b53e-f08c-49d0-ba42-5375f1307d2e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Configurare le metriche di fatturazione{#configure-billing-metrics}

Se utilizzi la configurazione predefinita, non è necessario fare altro per abilitare o configurare la fatturazione. Se avete ottenuto diversi parametri di configurazione dal rappresentante Adobe Enablement, utilizzate la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.

La maggior parte dei clienti deve utilizzare la configurazione predefinita.

>[!IMPORTANT]
>
>La configurazione impostata rimane attiva per tutta la durata del lettore multimediale. Una volta inizializzato il lettore multimediale, non è possibile modificare la configurazione.

Per configurare le metriche di fatturazione:

* Inserire il seguente esempio di codice.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   dove `_player` è un&#39;istanza di `AdobePSDK.MediaPlayer` e `_resource` è un&#39;istanza di `AdobePSDK.MediaResource`.

