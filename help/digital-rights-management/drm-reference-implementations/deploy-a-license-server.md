---
title: Distribuire il server licenze
description: Distribuire il server licenze
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Distribuire il server licenze{#deploy-the-license-server}

1. Copia i file di riferimento di implementazione in `webapps` sul server Tomcat.

   Per utilizzare il server licenze di implementazione di riferimento così com&#39;è, è sufficiente copiare il file WAR del server licenze ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) al `webapps` sul server Tomcat.

   Se si sta personalizzando il server licenze di implementazione di riferimento, copiare i file .war del server creati da `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` al `webapps` directory.

   >[!NOTE]
   >
   >Se in precedenza sono stati distribuiti i file WAR del server licenze, potrebbe essere necessario eliminare le directory WAR decompresse in [!DNL webapps] sul server Tomcat:
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]

   >[!NOTE]
   >
   >Non distribuire [!DNL edsws.war] a meno che non sia necessaria la retrocompatibilità con il contenuto di Flash Media Rights Management (FMRMS) v1.5. (Si tratta di un requisito molto raro).
   >
   >Se si preferisce impedire a Tomcat di decomprimere i file WAR, modificare `server.xml` nel `conf` directory e impostazione `unpackWARs` a `false`.

1. Copia l’intero contenuto della sezione `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` directory nel tuo [!DNL tomcat] directory.

   Il [!DNL resources] La directory include:

   * [!DNL flashaccesstools.properties] - File delle proprietà del server licenze.
   * [!DNL log4j.xml] - Configurazione registrazione server licenze
   * [!DNL *.pol] - File di criteri DRM di esempio.

   Inoltre, puoi anche scegliere di copiare i file di certificazione Adobe in questa posizione.

1. Modificare le impostazioni del server licenze in [!DNL flashaccesstools.properties] per riflettere la configurazione del server.

   Imposta come minimo i valori per le seguenti proprietà:

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

1. Modifica il `catalina.properties` file in Tomcat `conf` directory; aggiungi il percorso del [!DNL resources] (o il percorso alternativo in cui hai memorizzato il file delle proprietà e altri file di risorse) in `shared.loader` proprietà.

   Ad esempio, se hai `flashaccess-refimpl.properties` si trova in [!DNL [Tomcat Home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   Questo luoghi `flashaccess-refimpl.properties` nel percorso di classe.
1. Assicurati che gli altri file di risorse ( [!DNL log4j.xml], file di criteri, certificazioni) si trovano nel [!DNL resources] o si trovano in altro modo nel percorso di classe e la loro posizione specificata in [!DNL flashaccess-refimpl.properties].

   Inizialmente si desidera eseguire `log4j` in modalità di debug. In entrata [!DNL log4j.xml], impostato `debug` su true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Dal Tomcat [!DNL bin] , avviare il server.

   Su Linux:

   ```
   catalina.sh start
   ```

   In Windows:

   ```
   catalina.bat start
   ```
