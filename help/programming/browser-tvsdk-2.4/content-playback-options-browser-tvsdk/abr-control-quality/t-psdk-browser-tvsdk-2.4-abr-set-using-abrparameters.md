---
description: È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.
title: Configurare velocità bit adattivi utilizzando ABRControlParameters
exl-id: 53ca8516-b449-46c8-baa9-9d0d5800b3c8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# Configurare velocità bit adattivi utilizzando ABRControlParameters{#configure-adaptive-bit-rates-using-abrcontrolparameters}

È possibile impostare i valori di controllo ABR solo con ABRControlParameters, ma è possibile crearne uno nuovo in qualsiasi momento.

Le seguenti condizioni si applicano a `ABRControlParameters`:

* È necessario fornire i valori per tutti i parametri al momento della costruzione.
* Non è possibile modificare i singoli valori dopo il tempo di costruzione.
* Se i parametri specificati non rientrano nell&#39;intervallo consentito, `ArgumentError` viene lanciato.

1. Determinare il criterio ABR:

   * `ABRControlParameters.CONSERVATIVE_POLICY`
   * `ABRControlParameters.MODERATE_POLICY`
   * `ABRControlParameters.AGGRESSIVE_POLICY`

1. Impostare i valori dei parametri ABR in `ABRControlParameters` e assegnarli a Media Player.

   ```js
   var abrParams = new AdobePSDK.ABRControlParameters(); 
   abrParams.initialBitRate = nInitialBitRate; 
   abrParams.minBitRate = nMinBitRate; 
   abrParams.maxBitRate = nMaxBitRate; 
   abrParams.abrPolicy = eABRPolicy; 
   player.abrControlParameters = abrParams;
   ```
