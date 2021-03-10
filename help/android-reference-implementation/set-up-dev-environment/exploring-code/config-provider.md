---
description: La classe ConfigProvider ottiene la configurazione per il lettore multimediale. È necessario implementare l’interfaccia di configurazione in modo che i gestori di funzionalità possano leggere le informazioni di configurazione.
title: ConfigProvider
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# ConfigProvider {#configprovider}

La classe ConfigProvider ottiene la configurazione per il lettore multimediale. È necessario implementare l’interfaccia di configurazione in modo che i gestori di funzionalità possano leggere le informazioni di configurazione.

Utilizza la classe [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) per implementare le interfacce di configurazione `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig` e `IQosConfig` in modo che i responsabili delle funzioni possano leggere le configurazioni. Ad esempio, `ICCConfig` è l&#39;interfaccia per la configurazione `CCManager`. I file di configurazione ricevono i parametri di configurazione dal file di configurazione JSON.

Il file `ConfigProvider.java` è un esempio di implementazione di Adobe delle interfacce di configurazione. Legge le impostazioni da `SharedPreferences`, dove viene memorizzata la configurazione. Puoi archiviare la configurazione in qualsiasi modo che funzioni per la tua organizzazione. L&#39;implementazione della configurazione fornisce un wrapper per la tua origine di configurazione.