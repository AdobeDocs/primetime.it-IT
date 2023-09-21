---
description: La classe ConfigProvider ottiene la configurazione per il lettore multimediale. È necessario implementare l'interfaccia di configurazione in modo che i gestori di funzionalità possano leggere le informazioni di configurazione.
title: ConfigProvider
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# ConfigProvider {#configprovider}

La classe ConfigProvider ottiene la configurazione per il lettore multimediale. È necessario implementare l&#39;interfaccia di configurazione in modo che i gestori di funzionalità possano leggere le informazioni di configurazione.

Utilizzi il [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) classe per implementare `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig`, e `IQosConfig` le interfacce di configurazione in modo che i gestori di funzionalità possano leggere le configurazioni. Ad esempio, il `ICCConfig` è l&#39;interfaccia per `CCManager` configurazione. I file di configurazione ricevono i parametri di configurazione dal file di configurazione JSON.

Il `ConfigProvider.java` Questo file è un esempio di implementazione delle interfacce di configurazione da parte di Adobe. Legge le impostazioni da `SharedPreferences`, in cui è memorizzata la configurazione. Puoi archiviare la configurazione in qualsiasi modo che funzioni per la tua organizzazione. L&#39;implementazione della configurazione fornisce un wrapper per l&#39;origine di configurazione.
