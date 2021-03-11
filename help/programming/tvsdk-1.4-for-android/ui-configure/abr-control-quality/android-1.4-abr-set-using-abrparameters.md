---
description: È possibile impostare valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.
title: Configurare i bit rate adattivi utilizzando ABRControlParameters
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Configura i bit rate adattivi utilizzando ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

È possibile impostare valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.

Le seguenti condizioni si applicano a `ABRControlParameters`:

* È necessario fornire valori per tutti i parametri in fase di costruzione.
* Non è possibile modificare singoli valori dopo il tempo di costruzione.
* Se i parametri specificati sono al di fuori dell’intervallo consentito, viene lanciato un `ArgumentError`.

1. Decidere i bit rate iniziali, minimi e massimi.
1. Determina il criterio ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Imposta i valori dei parametri ABR nel costruttore `ABRControlParameters` e assegnali a Media Player.

   ```java
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```

