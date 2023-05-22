---
description: È possibile scegliere un punto di partenza personalizzato per l'immissione di un flusso DVR anziché il comportamento predefinito dell'immissione del flusso DVR all'inizio utilizzando la classe ConfigProvider.
title: Scelta di un punto di partenza personalizzato per il DVR
exl-id: 9813bf60-a91d-4376-a5fe-02311b73e8a0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Scelta di un punto di partenza personalizzato per il DVR {#choosing-a-custom-starting-point-for-dvr}

È possibile scegliere un punto di partenza personalizzato per l&#39;immissione di un flusso DVR anziché il comportamento predefinito dell&#39;immissione del flusso DVR all&#39;inizio utilizzando la classe ConfigProvider.

Per impostare l&#39;ora di inizio attraverso [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) classe:

1. Abilita [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. Impostare l&#39;ora di inizio in [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. Verifica che la posizione iniziale personalizzata sia abilitata.
