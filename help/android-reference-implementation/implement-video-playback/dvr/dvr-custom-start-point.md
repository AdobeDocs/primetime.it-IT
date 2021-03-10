---
description: È possibile scegliere un punto di partenza personalizzato per quando inserire un flusso DVR invece del comportamento predefinito di immissione del flusso DVR all'inizio utilizzando la classe ConfigProvider.
title: Scelta di un punto di partenza personalizzato per il DVR
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---


# Scelta di un punto di partenza personalizzato per il DVR {#choosing-a-custom-starting-point-for-dvr}

È possibile scegliere un punto di partenza personalizzato per quando inserire un flusso DVR invece del comportamento predefinito di immissione del flusso DVR all&#39;inizio utilizzando la classe ConfigProvider.

Per impostare l&#39;ora di inizio attraverso la classe [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) :

1. Abilita [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. Imposta l&#39;ora di inizio in [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. Verifica che la posizione iniziale personalizzata sia abilitata.
