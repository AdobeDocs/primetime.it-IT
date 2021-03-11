---
title: Proprietà del sistema Java
description: Proprietà del sistema Java
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Proprietà del sistema Java {#java-system-properties}

È possibile impostare facoltativamente le due seguenti proprietà di Java System per modificare il percorso della configurazione e dei file di registro per il server licenze:

* *LicenseServer.ConfigRoot* : directory contenente tutti i file di configurazione per il server licenze. Per informazioni dettagliate sul contenuto di questi file, vedere &quot;[File di configurazione del server di licenza](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)&quot;. Se non è impostato, il valore predefinito è *CATALINA_BASE/licenzieserver*.
* *LicenseServer.LogRoot* — Directory della cartella &quot;logs&quot;, in cui vengono scritti i log dell&#39;applicazione del server licenze. Se non è impostato, il valore predefinito è *LicenseServer.ConfigRoot*.

Se utilizzi [!DNL catalina.bat] o [!DNL catalina.sh] per avviare Tomcat, queste proprietà di sistema possono essere facilmente impostate utilizzando la variabile di ambiente `JAVA_OPTS`. Tutte le opzioni Java impostate qui verranno utilizzate all’avvio di Tomcat. Ad esempio, imposta:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

