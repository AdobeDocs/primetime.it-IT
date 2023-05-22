---
description: È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.
title: Configurare velocità bit adattivi utilizzando ABRControlParameters
exl-id: 787e962c-371f-4ac8-ae13-8b38a230593f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Configurare velocità bit adattivi utilizzando ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.

Le seguenti condizioni si applicano a `ABRControlParameters`:

* È necessario fornire i valori per tutti i parametri al momento della costruzione.
* Non è possibile modificare i singoli valori dopo il tempo di costruzione.
* Se i parametri specificati non rientrano nell&#39;intervallo consentito, `ArgumentError` viene lanciato.

1. Decidi la velocità di trasmissione iniziale, minima e massima.
1. Determinare il criterio ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Impostare i valori dei parametri ABR in `ABRControlParameters` e assegnarli a Media Player.

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
