---
title: Proprietà del sistema Java
description: Proprietà del sistema Java
copied-description: true
exl-id: 3fac8fac-7c71-4638-a671-eecc203dc871
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Proprietà del sistema Java {#java-system-properties}

Le due seguenti proprietà del sistema Java possono essere impostate facoltativamente per modificare la posizione dei file di configurazione e di registro per il server licenze:

* *LicenseServer.ConfigRoot* — Directory contenente tutti i file di configurazione per il server licenze. Per informazioni dettagliate sul contenuto di questi file, vedere &quot;[File di configurazione del server licenze](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)&quot;. Se non viene impostato, il valore predefinito è *CATALINA_BASE/LICENSeserver*.
* *LicenseServer.LogRoot* — Directory della cartella &quot;logs&quot;, in cui vengono scritti i log dell&#39;applicazione del server licenze. Se non viene impostato, il valore predefinito è *LicenseServer.ConfigRoot*.

Se sta usando [!DNL catalina.bat] o [!DNL catalina.sh] per avviare Tomcat, è possibile impostare facilmente queste proprietà di sistema utilizzando `JAVA_OPTS` variabile di ambiente. Tutte le opzioni Java qui impostate verranno utilizzate all’avvio di Tomcat. Ad esempio, imposta:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
