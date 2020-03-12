---
description: È possibile scegliere un punto di partenza personalizzato per specificare quando immettere un flusso DVR anziché il comportamento predefinito per l'immissione del flusso DVR all'inizio tramite la classe ConfigProvider.
seo-description: È possibile scegliere un punto di partenza personalizzato per specificare quando immettere un flusso DVR anziché il comportamento predefinito per l'immissione del flusso DVR all'inizio tramite la classe ConfigProvider.
seo-title: Scelta di un punto di partenza personalizzato per il DVR
title: Scelta di un punto di partenza personalizzato per il DVR
uuid: a7e13865-2b86-4234-ac4c-9a5320b293db
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Scelta di un punto di partenza personalizzato per il DVR {#choosing-a-custom-starting-point-for-dvr}

È possibile scegliere un punto di partenza personalizzato per specificare quando immettere un flusso DVR anziché il comportamento predefinito per l&#39;immissione del flusso DVR all&#39;inizio tramite la classe ConfigProvider.

Per impostare l&#39;ora di inizio attraverso la classe [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) :

1. Abilita [isCustomPositionPrefEnabled()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html#isCustomPositionPrefEnabled()).
1. Impostate l&#39;ora di inizio in [retrieveStartTimePref()](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/IPlaybackConfig.html#iretrieveStartTimePref()).
1. Verificate che la posizione iniziale personalizzata sia abilitata.
