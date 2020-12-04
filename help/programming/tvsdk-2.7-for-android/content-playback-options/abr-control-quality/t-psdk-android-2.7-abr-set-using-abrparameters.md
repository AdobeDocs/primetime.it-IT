---
description: È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.
seo-description: È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.
seo-title: Configurare i bitrate adattivi mediante ABRControlParameters
title: Configurare i bitrate adattivi mediante ABRControlParameters
uuid: 7084e954-196b-492e-846f-f8b36bed13a9
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Configurare i bitrate adattivi utilizzando ABRControlParameters {#configure-adaptive-bit-rates-using-abrcontrolparameters}

È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.

Le seguenti condizioni si applicano a `ABRControlParameters`:

* In fase di costruzione, è necessario fornire valori per tutti i parametri.
* Dopo la costruzione, non è possibile modificare i singoli valori.
* Se i parametri specificati non rientrano nell&#39;intervallo consentito, viene restituito un `ArgumentError`.

1. Consente di definire i bitrate iniziali, minimi e massimi.
1. Determinare il criterio ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Impostate i valori dei parametri ABR nel costruttore `ABRControlParameters` e assegnate i valori a Media Player.

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

