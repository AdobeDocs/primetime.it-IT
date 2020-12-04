---
description: La classe ConfigProvider ottiene la configurazione per il lettore multimediale. È necessario implementare l’interfaccia di configurazione in modo che i manager delle funzioni possano leggere le informazioni di configurazione.
seo-description: La classe ConfigProvider ottiene la configurazione per il lettore multimediale. È necessario implementare l’interfaccia di configurazione in modo che i manager delle funzioni possano leggere le informazioni di configurazione.
seo-title: ConfigProvider
title: ConfigProvider
uuid: 2467a617-6413-4b5d-9710-894cdc751b26
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# ConfigProvider {#configprovider}

La classe ConfigProvider ottiene la configurazione per il lettore multimediale. È necessario implementare l’interfaccia di configurazione in modo che i manager delle funzioni possano leggere le informazioni di configurazione.

È possibile utilizzare la classe [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) per implementare le interfacce di configurazione `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig` e `IQosConfig` in modo che i manager delle funzioni possano leggere le configurazioni. Ad esempio, `ICCConfig` è l&#39;interfaccia per la configurazione `CCManager`. I file di configurazione ricevono i parametri di configurazione dal file di configurazione JSON.

Il file `ConfigProvider.java` è un esempio &#39;implementazione  delle interfacce di configurazione. Vengono lette le impostazioni da `SharedPreferences`, dove è memorizzata la configurazione. Potete archiviare la configurazione in qualsiasi modo che funzioni per la vostra organizzazione. L&#39;implementazione della configurazione fornisce un wrapper per l&#39;origine di configurazione.