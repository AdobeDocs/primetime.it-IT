---
seo-title: Configurare e implementare il server per lo streaming protetto
title: Configurare e implementare il server per lo streaming protetto
uuid: 300a1b63-0bf0-48a8-977d-212563025c19
translation-type: tm+mt
source-git-commit: e60d285b9e30cdd19728e3029ecda995cd100ac9

---


# Configurare e implementare il server per lo streaming protetto {#set-up-and-deploy-the-server-for-protected-streaming}

1. Impostate la cartella di configurazione sul DVD DRM Primetime:

   `\Adobe Access Server for Protected Streaming\configs\`
1. Copiate la cartella di esempio `configs` nella cartella `<Tomcat_installation_dir>` e rinominatela in `licenseserver`.

   Il percorso della cartella configs deve ora essere `<Tomcat_install_dir>\licenseserver\`.
1. Eseguire `Scrambler.bat` per ottenere le password crittografate per i file PFX del server di trasporto e licenza nella directory DRM `<DVD>` di Primetime `\Adobe Access Server for Protected Streaming\` :

   * `Scrambler.bat <Adobe-provided transport credential password>`
   * `Scrambler.bat <Adobe-provided license server credential password>`

1. Copiate i file PFX nella `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\<tenant-name>\` directory.
1. Modificate la configurazione tenant corrispondente in `<TomcatInstallDir>\licenseserver\flashaccessserver\tenants\sampletenant\flashaccess-tenant.xml`, con le seguenti impostazioni:

   ```
   Configuration|Tenant|Credentials|TransportCredential|File|path=<filename-transport-credential-PFX> 
   Configuration|Tenant|Credentials|TransportCredential|File|password=<scrambled-transportcredential-password> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|path=<fielname-license-servercredential-PFX> 
   Configuration|Tenant|Credentials|LicenseServerCredential|File|password=<scrambled-license-servercredential-password>
   ```

1. Eseguire l&#39; `Validator.bat` utility per verificare la validità della configurazione:

   ```
   Validator.bat -g -r <absolute-path-to TomcatInstallDir\licenseserver>
   ```

1. Copiare il `flashaccessserver.war` file dal CD alla `<TomcatInstallDir>\webapps\` directory.
1. Se Tomcat è in esecuzione, arrestare l&#39;istanza Tomcat in esecuzione premendo `<CTRL-C>` nella finestra del comando (se è stata avviata dalla finestra del comando). È inoltre possibile arrestare il server dall&#39;applicazione Windows Services se Tomcat è stato installato come servizio Windows.
1. Per avviare Tomcat, immettete il comando seguente:

   ```
   <TomcatInstallDir>\bin\catalina run
   ```

1. Per verificare la configurazione, immettete il seguente URL in un browser:

   ```
    https://<LicenseServer>:8080/flashaccessserver/flashaccess/license/v2
   ```
