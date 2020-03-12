---
description: Se utilizzi la configurazione predefinita, non è necessario fare altro per abilitare o configurare la fatturazione. Se avete ottenuto diversi parametri di configurazione dal rappresentante Adobe Enablement, utilizzate la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.
seo-description: Se utilizzi la configurazione predefinita, non è necessario fare altro per abilitare o configurare la fatturazione. Se avete ottenuto diversi parametri di configurazione dal rappresentante Adobe Enablement, utilizzate la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.
seo-title: Configurare le metriche di fatturazione
title: Configurare le metriche di fatturazione
uuid: 340439bf-185b-4761-a481-010908842811
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

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

Inserire il seguente esempio di codice.

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
