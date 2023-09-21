---
description: È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.
title: Configurare velocità bit adattivi utilizzando ABRControlParameters
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Configurare velocità bit adattivi utilizzando ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.

Le seguenti condizioni si applicano a `ABRControlParameters`:

* Al momento della costruzione, dovete fornire i valori per tutti i parametri.
* Dopo la costruzione, non è possibile modificare i singoli valori.
* Se i parametri specificati non rientrano nell&#39;intervallo consentito, `ArgumentError` viene lanciato.

1. Determinare la velocità di trasmissione iniziale, minima e massima.
1. Determinare il criterio ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Impostare i valori dei parametri ABR in `ABRControlParameters` e assegnare i valori al lettore multimediale.

   ```
   public ABRControlParameters(int initialBitRate, 
     int minBitRate, 
     int maxBitRate, 
     ABRControlParameters.ABRPolicy abrPolicy, 
     int minTrickPlayBitRate, 
     int maxTrickPlayBitRate, 
     int maxTrickPlayBandwidthUsage, 
     int maxPlayoutRate);
   ```
