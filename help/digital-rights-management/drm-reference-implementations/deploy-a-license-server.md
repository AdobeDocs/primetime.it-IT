---
description: 'null'
seo-description: 'null'
seo-title: Distribuzione del server licenze
title: Distribuzione del server licenze
uuid: bee7ead1-ed13-4894-80f9-5196bf2f818f
translation-type: tm+mt
source-git-commit: 29149594c4b41956a091ef27093304e74ff15f2f

---


# Distribuzione del server licenze{#deploy-the-license-server}

1. Copiate i file di guerra di implementazione di riferimento nella `webapps` directory sul server Tomcat.

   Per utilizzare il server licenze di implementazione di riferimento così com&#39;è, è sufficiente copiare il file WAR del server licenze ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) nella `webapps` directory del server Tomcat.

   Se state personalizzando il server licenze di implementazione di riferimento, copiate i file di guerra del server generati `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` nella `webapps` directory.

   >[!NOTE]
   >
   >Se in precedenza avete distribuito file WAR del server licenze, potrebbe essere necessario eliminare le directory WAR non compresse nella [!DNL webapps] directory sul server Tomcat:        >
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >Non eseguite la distribuzione [!DNL edsws.war] , a meno che non sia necessaria la compatibilità con il contenuto Flash Media Rights Management (FMRMS) v1.5. (Questo è un requisito molto raro.)
   >
   >Se preferite impedire a Tomcat di disfare i file WAR, modificate `server.xml` nella `conf` directory e impostate `unpackWARs` su `false`.

1. Copiate l’intero contenuto della `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` directory nella [!DNL tomcat] directory.

   La [!DNL resources] directory include:

   * [!DNL flashaccesstools.properties] - Il file delle proprietà del server licenze.
   * [!DNL log4j.xml] - Configurazione registrazione server licenze
   * [!DNL *.pol] - File di criteri DRM di esempio.
   Inoltre, potete anche scegliere di copiare i file di certificazione Adobe in questa posizione.

1. Modificate le impostazioni del server licenze in [!DNL flashaccesstools.properties] modo da riflettere la configurazione del server.

   Come minimo, impostate i valori per le seguenti proprietà:

   * `config.resourcesDirectory`
   * `HandlerConfiguration.ServerTransportCredential`
   * `HandlerConfiguration.ServerTransportCredential.password`
   * `LicenseHandler.ServerCredential`
   * `LicenseHandler.ServerCredential.password`
   * `MetaDataConverter.SignatureParameters.ServerCredential`
   * `MetaDataConverter.SignatureParameters.ServerCredential.password`
   * `V2KeyParameters.LicenseServerUrl`
   * `V2KeyParameters.KeyOptions.AsymmetricKeyOptions.Certificate`
   * V2KeyParameters.LicenseServerTransportCertificate

1. Modificate il `catalina.properties` file nella directory Tomcat `conf` ; aggiungete alla [!DNL resources] proprietà il percorso della `shared.loader` directory (o il percorso alternativo in cui avete memorizzato il file delle proprietà e altri file di risorse).

   Ad esempio, se si `flashaccess-refimpl.properties` trova in [!DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   Viene posizionato `flashaccess-refimpl.properties` sul percorso di classe.
1. Verificate che gli altri file di risorse ( [!DNL log4j.xml]file di criteri, certificazioni) si trovino nella [!DNL resources] directory oppure che si trovino nel percorso di classe e nella posizione specificata in [!DNL flashaccess-refimpl.properties].

   È probabile che si desideri eseguire inizialmente `log4j` in modalità debug. In [!DNL log4j.xml], impostate `debug` su true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Dalla directory Tomcat [!DNL bin] , avviate il server.

   In Linux:

   ```
   catalina.sh start
   ```

   In Windows:

   ```
   catalina.bat start
   ```
