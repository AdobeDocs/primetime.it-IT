---
seo-title: Proprietà del sistema Java
title: Proprietà del sistema Java
uuid: ad1f3d9b-7d95-4e19-a0f8-fd7d4dd4dc32
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Proprietà del sistema Java {#java-system-properties}

È possibile impostare facoltativamente le due seguenti proprietà di Java System per modificare il percorso di configurazione e i file di registro per il server licenze:

* *LicenseServer.ConfigRoot* — Directory contenente tutti i file di configurazione per il server licenze. Per informazioni dettagliate sul contenuto di questi file, vedere &quot;[File di configurazione del server licenze](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)&quot;. Se non è impostato, il valore predefinito è *CATALINA_BASE/licenzieserver*.
* *LicenseServer.LogRoot* — Directory della cartella &quot;logs&quot;, in cui vengono scritti i registri delle applicazioni del server licenze. Se non è impostato, il valore predefinito è *LicenseServer.ConfigRoot*.

Se si utilizza [!DNL catalina.bat] o [!DNL catalina.sh] per avviare Tomcat, queste proprietà di sistema possono essere facilmente impostate utilizzando la variabile di ambiente `JAVA_OPTS`. Tutte le opzioni Java impostate qui verranno utilizzate all&#39;avvio di Tomcat. Ad esempio, set:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

