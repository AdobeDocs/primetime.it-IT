---
description: Utilizza la funzione External CEK per vendere e creare pacchetti di licenze utilizzando il tuo CKMS esistente.
title: Utilizzo di CEK esterno per le licenze Vend e Package
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---


# Utilizzo di CEK esterno per inviare e creare pacchetti di licenze{#using-external-cek-to-vend-and-package-licenses}

Utilizza la funzione External CEK per vendere e creare pacchetti di licenze utilizzando il tuo CKMS esistente.

## EncryptContentWithExternalKey.java

Si tratta di uno strumento a riga di comando che crittografa un video in formato AAXS e crea metadati che *non* conterranno il CEK (protetto con il certificato pubblico di un server di licenze AAXS). Lo strumento incorpora invece un CEK ID nei metadati del video.

Durante l&#39;acquisizione della licenza, il server licenze AAXS osserva un flag nei metadati che identifica che il contenuto è stato protetto utilizzando un CEK esterno. Il server licenze estrae l’ID CEK dai metadati, quindi esegue una query su un archivio protetto/CKMS per recuperare il CEK appropriato.

## Flusso di lavoro di pacchetto

1. Assicurati di utilizzare Java 1.6.0_24 o versione successiva.
1. Per visualizzare l’utilizzo dello strumento: `java -jar AdobePackager_ExternalCEK.jar`
1. Per creare un pacchetto di contenuti:

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* Il codice sorgente Java può essere generato utilizzando l&#39;ANT incluso `build-samples.xml`
>* L&#39;SDK del Flash Access ( `adobe-flashaccess-sdk.jar`) deve trovarsi nel percorso di classe

>



## Flusso di lavoro del server

1. Imposta l&#39;implementazione di riferimento.
1. Se esistono, elimina le implementazioni precedenti di Implementazione dei riferimenti:

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. Verifica che sia presente un file [!DNL CEKDepot.properties] accanto al tuo [!DNL flashaccess-refimpl.properties]

1. Avviare una richiesta di licenza da un Adobe Primetime Player
1. Osserva i registri di Impl degli Rif per qualcosa di simile:

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. Potrebbe essere necessario modificare le impostazioni [!DNL log4j.xml] per registrare a un livello `DEBUG` ( `INFO` è impostato per impostazione predefinita)

## Problemi noti

Nessuno
