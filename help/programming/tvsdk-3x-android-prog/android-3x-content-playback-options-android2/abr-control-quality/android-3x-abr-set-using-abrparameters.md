---
description: È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.
seo-description: È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.
seo-title: Configurare i bitrate adattivi mediante ABRControlParameters
title: Configurare i bitrate adattivi mediante ABRControlParameters
uuid: 283ccd3d-535b-43ca-8ca5-82d12df31798
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Configurare i bitrate adattivi mediante ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.

Le seguenti condizioni si applicano a `ABRControlParameters`:

* In fase di costruzione, è necessario fornire valori per tutti i parametri.
* Dopo la costruzione, non è possibile modificare i singoli valori.
* Se i parametri specificati non rientrano nell&#39;intervallo consentito, `ArgumentError` viene generato un errore.

1. Consente di definire i bitrate iniziali, minimi e massimi.
1. Determinare il criterio ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Impostate i valori dei parametri ABR nel `ABRControlParameters` costruttore e assegnate i valori a Media Player.

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
