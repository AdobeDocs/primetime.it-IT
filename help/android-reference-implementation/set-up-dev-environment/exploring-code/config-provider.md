---
description: La classe ConfigProvider ottiene la configurazione per il lettore multimediale. È necessario implementare l'interfaccia di configurazione in modo che i gestori di funzionalità possano leggere le informazioni di configurazione.
title: ConfigProvider
exl-id: 75613bfb-3c2b-4b53-b365-adc98f7e1164
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# ConfigProvider {#configprovider}

La classe ConfigProvider ottiene la configurazione per il lettore multimediale. È necessario implementare l&#39;interfaccia di configurazione in modo che i gestori di funzionalità possano leggere le informazioni di configurazione.

Utilizzi il [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) classe per implementare `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig`, e `IQosConfig` le interfacce di configurazione in modo che i gestori di funzionalità possano leggere le configurazioni. Ad esempio, il `ICCConfig` è l&#39;interfaccia per `CCManager` configurazione. I file di configurazione ricevono i parametri di configurazione dal file di configurazione JSON.

Il `ConfigProvider.java` Questo file è un esempio di implementazione delle interfacce di configurazione da parte di Adobe. Legge le impostazioni da `SharedPreferences`, in cui è memorizzata la configurazione. Puoi archiviare la configurazione in qualsiasi modo che funzioni per la tua organizzazione. L&#39;implementazione della configurazione fornisce un wrapper per l&#39;origine di configurazione.
