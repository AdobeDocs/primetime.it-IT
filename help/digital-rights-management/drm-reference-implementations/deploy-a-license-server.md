---
description: 'null'
seo-description: 'null'
seo-title: Distribuzione del server licenze
title: Distribuzione del server licenze
uuid: bee7ead1-ed13-4894-80f9-5196bf2f818f
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Distribuzione del server licenze{#deploy-the-license-server}

1. Copiate i file di guerra di implementazione di riferimento nella directory `webapps` sul server Tomcat.

   Per utilizzare il server licenze di implementazione di riferimento così com&#39;è, è sufficiente copiare il file WAR del server licenze ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) nella directory `webapps` sul server Tomcat.

   Se state personalizzando il server licenze di implementazione di riferimento, copiate i file di guerra del server generati da `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` nella directory `webapps`.

   >[!NOTE]
   >
   >Se avete precedentemente distribuito file WAR del server licenze, potrebbe essere necessario eliminare le directory WAR non compresse nella directory [!DNL webapps] sul server Tomcat:
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >Non distribuire [!DNL edsws.war] a meno che non sia necessaria la compatibilità con contenuti FMRMS (Flash Media Rights Management) v1.5. (Questo è un requisito molto raro.)
   >
   >Se si preferisce impedire a Tomcat di disfare i file WAR, modificare `server.xml` nella directory `conf` e impostare `unpackWARs` su `false`.

1. Copiate l&#39;intero contenuto della directory `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` nella directory [!DNL tomcat].

   La directory [!DNL resources] include:

   * [!DNL flashaccesstools.properties] - Il file delle proprietà del server licenze.
   * [!DNL log4j.xml] - Configurazione registrazione server licenze
   * [!DNL *.pol] - File di criteri DRM di esempio.

   Inoltre, potete anche scegliere di copiare i file di certificazione  Adobe in questa posizione.

1. Modificate le impostazioni del server licenze in [!DNL flashaccesstools.properties] per riflettere la configurazione del server.

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

1. Modificate il file `catalina.properties` nella directory Tomcat `conf`; aggiungere la posizione della directory [!DNL resources] (o la posizione alternativa in cui sono stati memorizzati i file delle proprietà e altri file di risorse) alla proprietà `shared.loader`.

   Ad esempio, se `flashaccess-refimpl.properties` si trova in [!DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   Posiziona `flashaccess-refimpl.properties` nel percorso di classe.
1. Verificate che gli altri file di risorse ( [!DNL log4j.xml], i file dei criteri e le certificazioni) si trovino nella directory [!DNL resources] oppure siano nel percorso di classe e nella posizione specificata in [!DNL flashaccess-refimpl.properties].

   È probabile che si desideri eseguire inizialmente `log4j` in modalità di debug. In [!DNL log4j.xml], impostare `debug` su true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Dalla directory Tomcat [!DNL bin], avviate il server.

   In Linux:

   ```
   catalina.sh start
   ```

   In Windows:

   ```
   catalina.bat start
   ```
