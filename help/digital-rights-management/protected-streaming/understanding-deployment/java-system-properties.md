---
description: Sul server licenze è possibile configurare diverse proprietà del sistema Java per controllare la posizione dei file di configurazione e di registro.
title: Proprietà del sistema Java
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Proprietà del sistema Java{#java-system-properties}

Sul server licenze è possibile configurare diverse proprietà del sistema Java per controllare la posizione dei file di configurazione e di registro.

Facoltativamente, puoi configurare le seguenti proprietà del sistema Java:

* *`LicenseServer.ConfigRoot`* — Nome della directory che include i file di configurazione per il server licenze.

   Per informazioni dettagliate sul contenuto di questi file, consulta *Licenza file di configurazione del server* . Se non è configurato, il valore predefinito è `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot* : nome della  [!DNL logs] directory in cui si trovano i log dell&#39;applicazione del server licenze. Se il nome di questa directory non è stato modificato, per impostazione predefinita il nome di questa directory è configurato come *LicenseServer.ConfigRoot*.

Se utilizzi il file [!DNL catalina.bat] o [!DNL catalina.sh] per avviare Tomcat, puoi configurare le proprietà di sistema con la variabile di ambiente `JAVA_OPTS`. Tutte le opzioni Java configurate vengono applicate automaticamente all&#39;avvio di Tomcat.

Ad esempio, puoi configurare la variabile di ambiente `JAVA_OPTS` come segue:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```

