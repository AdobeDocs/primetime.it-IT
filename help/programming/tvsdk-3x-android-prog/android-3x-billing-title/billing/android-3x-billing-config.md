---
description: Se utilizzi la configurazione predefinita, non c’è altro da fare per abilitare o configurare la fatturazione. Se hai ottenuto parametri di configurazione diversi dal rappresentante Adobe Enablement, utilizza la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.
title: Configurare le metriche di fatturazione
exl-id: e3b97de6-8442-463f-b5b0-0dec34aa7735
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Configurare le metriche di fatturazione {#configure-billing-metrics}

Se utilizzi la configurazione predefinita, non c’è altro da fare per abilitare o configurare la fatturazione. Se hai ottenuto parametri di configurazione diversi dal rappresentante Adobe Enablement, utilizza la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.

>[!TIP]
>
>La maggior parte dei clienti deve utilizzare la configurazione predefinita.

>[!IMPORTANT]
>
>La configurazione impostata rimane attiva per tutta la durata del lettore multimediale. Una volta inizializzato il lettore multimediale, non è possibile modificare la configurazione.

Per configurare le metriche di fatturazione:

Inserire il codice di esempio seguente.

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
