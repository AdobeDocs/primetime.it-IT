---
description: È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.
seo-description: È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.
seo-title: Configurare i bitrate adattivi mediante ABRControlParameters
title: Configurare i bitrate adattivi mediante ABRControlParameters
uuid: c877c5cc-ad72-46dc-afc4-d41ee097a9a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---


# Configurare i bitrate adattivi utilizzando ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.

Le seguenti condizioni si applicano a `ABRControlParameters`:

* È necessario specificare i valori per tutti i parametri al momento della costruzione.
* Non è possibile modificare singoli valori dopo il tempo di costruzione.
* Se i parametri specificati non rientrano nell&#39;intervallo consentito, viene restituito un `ArgumentError`.

1. Decidete i bitrate iniziali, minimi e massimi.
1. Determinare il criterio ABR:

   * `ABR_CONSERVATIVE`
   * `ABR_MODERATE`
   * `ABR_AGGRESSIVE`

1. Impostate i valori dei parametri ABR nel costruttore `ABRControlParameters` e assegnateli a Media Player.

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

