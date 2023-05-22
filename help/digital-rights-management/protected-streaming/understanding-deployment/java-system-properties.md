---
description: Nel server licenze è possibile configurare diverse proprietà del sistema Java per controllare la posizione dei file di configurazione e di registro.
title: Proprietà del sistema Java
exl-id: 08fe6910-9d58-41c3-91d3-514406bedf05
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Proprietà del sistema Java{#java-system-properties}

Nel server licenze è possibile configurare diverse proprietà del sistema Java per controllare la posizione dei file di configurazione e di registro.

Facoltativamente, puoi configurare le seguenti proprietà del sistema Java:

* *`LicenseServer.ConfigRoot`* — Nome della directory che include i file di configurazione per il server licenze.

   Consulta *File di configurazione del server licenze* per informazioni dettagliate sul contenuto di questi file. Se non è configurato, il valore predefinito è `CATALINA_BASE/licenseserver`.

* *LicenseServer.LogRoot* — Nome del [!DNL logs] directory in cui si trovano i registri applicazioni del server licenze. Se non hai modificato il nome di questa directory, il nome della directory viene configurato come *LicenseServer.ConfigRoot* per impostazione predefinita.

Se si utilizza [!DNL catalina.bat] o [!DNL catalina.sh] per avviare Tomcat, è possibile configurare le proprietà di sistema con il `JAVA_OPTS` variabile di ambiente. Tutte le opzioni Java configurate vengono applicate automaticamente all&#39;avvio di Tomcat.

Ad esempio, puoi configurare `JAVA_OPTS` variabile di ambiente come segue:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
