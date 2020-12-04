---
description: Nel server delle licenze è possibile configurare diverse proprietà del sistema Java per controllare la posizione dei file di configurazione e di registro.
seo-description: Nel server delle licenze è possibile configurare diverse proprietà del sistema Java per controllare la posizione dei file di configurazione e di registro.
seo-title: Proprietà del sistema Java
title: Proprietà del sistema Java
uuid: d8c72359-bf61-47e0-9cd5-b21225d5fe49
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Proprietà del sistema Java{#java-system-properties}

Nel server delle licenze è possibile configurare diverse proprietà del sistema Java per controllare la posizione dei file di configurazione e di registro.

Facoltativamente, puoi configurare le seguenti proprietà di Java System:

* *`LicenseServer.ConfigRoot`* — Nome della directory che include i file di configurazione per il server licenze.

   Per informazioni dettagliate sul contenuto di questi file, vedere *File di configurazione del server licenze*. Se non è configurata, il valore predefinito è `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot* — Nome della  [!DNL logs] directory in cui si trovano i registri dell&#39;applicazione del server licenze. Se il nome di questa directory non è stato modificato, per impostazione predefinita il nome di questa directory è configurato come *LicenseServer.ConfigRoot*.

Se si utilizza il file [!DNL catalina.bat] o [!DNL catalina.sh] per avviare Tomcat, è possibile configurare le proprietà del sistema con la variabile di ambiente `JAVA_OPTS`. Tutte le opzioni Java configurate vengono applicate automaticamente all&#39;avvio di Tomcat.

Ad esempio, puoi configurare la variabile di ambiente `JAVA_OPTS` come segue:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

