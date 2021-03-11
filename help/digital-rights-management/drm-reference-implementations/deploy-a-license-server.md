---
title: Distribuzione del server licenze
description: Distribuzione del server licenze
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# Distribuire il server licenze{#deploy-the-license-server}

1. Copia i file di guerra di implementazione di riferimento nella directory `webapps` sul server Tomcat.

   Per utilizzare il server licenze di implementazione di riferimento così com&#39;è, è sufficiente copiare il file WAR del server licenze ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) nella directory `webapps` sul server Tomcat.

   Se stai personalizzando il server licenze di implementazione di riferimento, copia i file di guerra del server generati da `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` nella directory `webapps`.

   >[!NOTE]
   >
   >Se in precedenza sono stati distribuiti file WAR del server licenze, potrebbe essere necessario eliminare le directory WAR decompresse nella directory [!DNL webapps] sul server Tomcat:
   >
   >* [!DNL webapps/flashaccess]
   >* [!DNL webapps/edcws]


   >[!NOTE]
   >
   >Non distribuire [!DNL edsws.war] a meno che non sia necessaria la compatibilità con i contenuti FMRMS (Flash Media Rights Management) v1.5. (Questo è un requisito molto raro.)
   >
   >Se si preferisce evitare che Tomcat scompili i file WAR, modificare `server.xml` nella directory `conf` e impostare `unpackWARs` su `false`.

1. Copia l&#39;intero contenuto della directory `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` nella directory [!DNL tomcat].

   La directory [!DNL resources] include:

   * [!DNL flashaccesstools.properties] - Il file delle proprietà del server licenze.
   * [!DNL log4j.xml] - Configurazione della registrazione del server licenze
   * [!DNL *.pol] - File di criteri DRM di esempio.

   Inoltre, puoi anche scegliere di copiare i file di certificazione di Adobe in questo percorso.

1. Modifica le impostazioni del server licenze in [!DNL flashaccesstools.properties] per riflettere la configurazione del server.

   Come minimo, imposta i valori per le seguenti proprietà:

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

1. Modifica il file `catalina.properties` nella directory Tomcat `conf`; aggiungi la posizione della directory [!DNL resources] (o la posizione alternativa in cui è stato memorizzato il file delle proprietà e altri file di risorse) alla proprietà `shared.loader` .

   Ad esempio, se ti trovi `flashaccess-refimpl.properties` in [!DNL [Tomcat home]\resources\]:

   ```
   shared.loader=..\resources
   ```

   Questo posiziona `flashaccess-refimpl.properties` nel percorso di classe.
1. Assicurati che gli altri file di risorse ( [!DNL log4j.xml], file di criteri e certificazioni) si trovino nella directory [!DNL resources] o si trovino nel percorso di classe e nella posizione specificata in [!DNL flashaccess-refimpl.properties].

   È probabile che si desideri eseguire inizialmente `log4j` in modalità di debug. In [!DNL log4j.xml], impostare `debug` su true:

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. Dalla directory Tomcat [!DNL bin], avvia il server.

   Su Linux:

   ```
   catalina.sh start
   ```

   In Windows:

   ```
   catalina.bat start
   ```
