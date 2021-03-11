---
title: Configurazione e distribuzione del server per lo streaming protetto
description: Configurazione e distribuzione del server per lo streaming protetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# Configurare e distribuire il server per lo streaming protetto {#set-up-and-deploy-the-server-for-protected-streaming}

1. Impostare la cartella di configurazione sul DVD DRM Primetime:

   `\Adobe Access Server for Protected Streaming\configs\`
1. Copia la cartella di esempio `configs` nel `<Tomcat_installation_dir>` e rinomina la cartella copiata in `licenseserver`.

   Il percorso della cartella configs deve ora essere `<Tomcat_install_dir>\licenseserver\`.
1. Esegui `Scrambler.bat` per ottenere le password crittografate per i file PFX del server di trasporto e licenza nella directory DRM `<DVD>` `\Adobe Access Server for Protected Streaming\` di Primetime:

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. Copiare i file PFX nella directory `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\`.
1. Modifica la configurazione tenant corrispondente in `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`, con le seguenti impostazioni:

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. Esegui l&#39;utilità `Validator.bat` per verificare la validità della configurazione:

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. Copiare il file `flashaccessserver.war` dal CD nella directory `<TomcatInstallDir>\webapps\`.
1. Se Tomcat è in esecuzione, arresta l&#39;istanza Tomcat in esecuzione premendo `<CTRL-C>` nella finestra dei comandi (se è stata avviata dalla finestra dei comandi). È inoltre possibile arrestare il server dall&#39;applicazione Windows Services se Tomcat è stato installato come servizio Windows.
1. Per avviare Tomcat, immetti il seguente comando:

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. Per verificare la configurazione, immetti il seguente URL in un browser:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
