---
description: Se utilizzi la configurazione predefinita, non è necessario eseguire altre operazioni per abilitare o configurare la fatturazione. Se hai ottenuto diversi parametri di configurazione dal tuo rappresentante di abilitazione Adobe, utilizza la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.
title: Configurare le metriche di fatturazione
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Configura le metriche di fatturazione{#configure-billing-metrics}

Se utilizzi la configurazione predefinita, non è necessario eseguire altre operazioni per abilitare o configurare la fatturazione. Se hai ottenuto diversi parametri di configurazione dal tuo rappresentante di abilitazione Adobe, utilizza la classe BillingMetricsConfiguration per impostare questi parametri prima di inizializzare il lettore multimediale.

La maggior parte dei clienti deve utilizzare la configurazione predefinita.

>[!IMPORTANT]
>
>La configurazione impostata rimane attiva per tutta la durata del lettore multimediale. Una volta inizializzato il lettore multimediale, non è possibile modificare la configurazione.

Per configurare le metriche di fatturazione:

* Immetti il seguente codice di esempio.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.billingMetricsConfiguration.isEnabled = true; 
   config.billingMetricsConfiguration.proVODBillableDurationMinutes = 60; 
   config.billingMetricsConfiguration.stdVODBillableDurationMinutes = 30; 
   config.billingMetricsConfiguration.liveBillableDurationMinutes = 15; 
   _player.replaceCurrentResource(_resource, config);
   ```

   dove `_player` è un&#39;istanza di `AdobePSDK.MediaPlayer` e `_resource` è un&#39;istanza di `AdobePSDK.MediaResource`.

