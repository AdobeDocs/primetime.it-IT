---
description: Se utilizzi la configurazione predefinita, non è necessario fare altro per abilitare o configurare la fatturazione. Se avete ottenuto diversi parametri di configurazione dal rappresentante Adobe Enablement, utilizzate la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.
seo-description: Se utilizzi la configurazione predefinita, non è necessario fare altro per abilitare o configurare la fatturazione. Se avete ottenuto diversi parametri di configurazione dal rappresentante Adobe Enablement, utilizzate la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.
seo-title: Configurare le metriche di fatturazione
title: Configurare le metriche di fatturazione
uuid: d8656ab2-fdd8-4fe4-8578-a6c8ecd378e2
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Configurare le metriche di fatturazione {#configure-billing-metrics}

Se utilizzi la configurazione predefinita, non è necessario fare altro per abilitare o configurare la fatturazione. Se avete ottenuto diversi parametri di configurazione dal rappresentante Adobe Enablement, utilizzate la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.

>[!TIP]
>
>La maggior parte dei clienti deve utilizzare la configurazione predefinita.

>[!IMPORTANT]
>
>La configurazione impostata rimane attiva per tutta la durata del lettore multimediale. Una volta inizializzato il lettore multimediale, non è possibile modificare la configurazione.

Per configurare le metriche di fatturazione:

1. Inserire il seguente esempio di codice.

   ```java
   MediaPlayerItemConfig config = new MediaPlayerItemConfig(); 
   BillingMetricsConfiguration billingConfig = new BillingMetricsConfiguration(); 
   billingConfig.setEnabled(true); 
   billingConfig.setProVODBillableDurationMinutes(60); 
   billingConfig.setStdVODBillableDurationMinutes(30); 
   billingConfig.setLiveBillableDurationMinutes(15); 
   config.setBillingMetricsConfiguration(billingConfig); 
   mediaPlayer.replaceCurrentResource(mediaResource, config);
   ```

