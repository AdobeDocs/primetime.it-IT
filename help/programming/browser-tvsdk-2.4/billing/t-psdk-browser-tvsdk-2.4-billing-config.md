---
description: Se utilizzi la configurazione predefinita, non c’è altro da fare per abilitare o configurare la fatturazione. Se hai ottenuto parametri di configurazione diversi dal rappresentante Adobe Enablement, utilizza la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.
title: Configurare le metriche di fatturazione
exl-id: 1eb50822-77a0-4b3a-a84c-b6082bcd1cad
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Configurare le metriche di fatturazione{#configure-billing-metrics}

Se utilizzi la configurazione predefinita, non c’è altro da fare per abilitare o configurare la fatturazione. Se hai ottenuto parametri di configurazione diversi dal rappresentante Adobe Enablement, utilizza la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.

La maggior parte dei clienti deve utilizzare la configurazione predefinita.

>[!IMPORTANT]
>
>La configurazione impostata rimane attiva per tutta la durata del lettore multimediale. Una volta inizializzato il lettore multimediale, non è possibile modificare la configurazione.

Per configurare le metriche di fatturazione:

* Inserire il codice di esempio seguente.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   dove `_player` è un’istanza di `AdobePSDK.MediaPlayer` e `_resource` è un’istanza di `AdobePSDK.MediaResource`.
