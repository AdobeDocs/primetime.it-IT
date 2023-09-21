---
title: Configurazione e distribuzione del server per lo streaming protetto
description: Configurazione e distribuzione del server per lo streaming protetto
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Configurazione e distribuzione del server per lo streaming protetto {#set-up-and-deploy-the-server-for-protected-streaming}

1. Configurare la cartella di configurazione sul DVD DRM di Primetime:

   `\Adobe Access Server for Protected Streaming\configs\`
1. Copia l’esempio `configs` cartella al tuo `<Tomcat_installation_dir>` e rinominare la cartella copiata in `licenseserver`.

   Il percorso della cartella configs ora dovrebbe essere `<Tomcat_install_dir>\licenseserver\`.
1. Esegui `Scrambler.bat` per ottenere le password crittografate per i file PFX del server di trasporto e delle licenze nel DRM di Primetime `<DVD>` `\Adobe Access Server for Protected Streaming\` directory:

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. Copiare i file PFX in `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` directory.
1. Modificare la configurazione tenant corrispondente in `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`, con le seguenti impostazioni:

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. Esegui il `Validator.bat` l&#39;utilità per verificare la configurazione è valida:

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. Copia il `flashaccessserver.war` dal CD al `<TomcatInstallDir>\webapps\` directory.
1. Se Tomcat è in esecuzione, arrestare l&#39;istanza Tomcat in esecuzione premendo `<CTRL-C>` nella finestra di comando (se è stata avviata dalla finestra di comando). È inoltre possibile arrestare il server dall&#39;applicazione Servizi Windows se Tomcat è stato installato come servizio Windows.
1. Per avviare Tomcat, immetti il comando seguente:

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. Per verificare la configurazione, immetti il seguente URL in un browser:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
