---
description: Utilizza la funzione External CEK per vendere e creare pacchetti di licenze utilizzando il CKMS esistente.
title: Utilizzo di CEK esterno per le licenze di distribuzione e pacchetto
exl-id: 3944624a-099e-4fc0-b829-6ab154a53758
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Utilizzo di CEK esterno per le licenze di distribuzione e pacchetto{#using-external-cek-to-vend-and-package-licenses}

Utilizza la funzione External CEK per vendere e creare pacchetti di licenze utilizzando il CKMS esistente.

## EncryptContentWithExternalKey.java

Questo è uno strumento da riga di comando che consente ad AAXS di crittografare un video e creare metadati che *non* contiene il certificato CEK (protetto con il certificato pubblico di un server licenze AAXS). Al contrario, lo strumento incorpora un CEK ID nei metadati del video.

Durante l&#39;acquisizione della licenza, il server licenze AAXS osserva un flag nei metadati che identifica che il contenuto è stato protetto utilizzando un codice CEK esterno. Il server licenze estrarrà l&#39;ID CEK dai metadati e quindi eseguirà una query su un archivio protetto/CKMS per recuperare il CEK appropriato.

## Flusso di lavoro di creazione pacchetti

1. Assicurati di utilizzare Java 1.6.0_24 o versione successiva.
1. Per visualizzare l&#39;utilizzo dello strumento: `java -jar AdobePackager_ExternalCEK.jar`
1. Per creare un pacchetto di contenuto:

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* Il codice sorgente Java può essere creato utilizzando il codice ANT incluso `build-samples.xml`
>* SDK per Flash Access ( `adobe-flashaccess-sdk.jar`) deve trovarsi nel percorso di classe
>


## Flusso di lavoro del server

1. Imposta l’implementazione di riferimento.
1. Se ne esistono già, ripulisci le precedenti distribuzioni di implementazione di riferimento:

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. Verifica che sia presente [!DNL CEKDepot.properties] insieme al file [!DNL flashaccess-refimpl.properties]

1. Avviare una richiesta di licenza da un lettore Adobe Primetime
1. Osserva i registri di Impl dei riferimenti per qualcosa di simile a:

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. Potrebbe essere necessario modificare il [!DNL log4j.xml] impostazioni per l&#39;accesso `DEBUG` livello ( `INFO` è impostato per impostazione predefinita)

## Problemi noti

Nessuno
