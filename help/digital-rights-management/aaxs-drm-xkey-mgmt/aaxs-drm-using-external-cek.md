---
description: Utilizzate la funzione Esterno CEK per vendere e creare pacchetti di licenze utilizzando il vostro CKMS esistente.
seo-description: Utilizzate la funzione Esterno CEK per vendere e creare pacchetti di licenze utilizzando il vostro CKMS esistente.
seo-title: Utilizzo di licenze CEK esterne per Vend e Package
title: Utilizzo di licenze CEK esterne per Vend e Package
uuid: 1bfd8c6c-4ae9-47de-8247-085b5360127d
translation-type: tm+mt
source-git-commit: fe9493d610bc6fb97d30351c707b73cda92c67a0
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Utilizzo di licenze CEK esterne per Vend e Package{#using-external-cek-to-vend-and-package-licenses}

Utilizzate la funzione Esterno CEK per vendere e creare pacchetti di licenze utilizzando il vostro CKMS esistente.

## EncryptContentWithExternalKey.java

Si tratta di uno strumento della riga di comando che esegue la cifratura AAXS di un video e crea metadati che *non* contengono il CEK (protetto con il certificato pubblico di un server licenze AAXS). Al contrario, lo strumento incorpora un CEK ID nei metadati del video.

Durante l&#39;acquisizione della licenza, il server licenze AAXS osserva un flag nei metadati che identifica il contenuto protetto tramite un CEK esterno. Il server licenze estrae l’ID CEK dai metadati, quindi esegue una query su un repository protetto/CKMS per recuperare il CEK appropriato.

## Flusso di lavoro di creazione pacchetti

1. Assicurarsi di utilizzare Java 1.6.0_24 o versione successiva.
1. Per visualizzare l’utilizzo dello strumento: `java -jar AdobePackager_ExternalCEK.jar`
1. Per creare pacchetti di contenuto:

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* Il codice di origine Java può essere creato utilizzando l&#39;elemento ANT `build-samples.xml` incluso
>* L&#39;SDK del Flash Access ( `adobe-flashaccess-sdk.jar`) deve trovarsi nel percorso di classe

>



## Flusso di lavoro server

1. Configurare l&#39;implementazione di riferimento.
1. Se esiste, pulisci le precedenti distribuzioni di implementazione di riferimento:

   1. `delete <tomcat>\work\Catalina\*.*`
   1. `delete <tomcat>\conf\Catalina\*.*`
   1. `delete <tomcat>\logs\*.*`

1. Verificare che sia presente un file [!DNL CEKDepot.properties] accanto a [!DNL flashaccess-refimpl.properties]

1. Avviare una richiesta di licenza da un Adobe Primetime Player 
1. Osservare i registri degli indirizzi di riferimento per ottenere un risultato simile a:

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

   1. Potrebbe essere necessario modificare le impostazioni [!DNL log4j.xml] per eseguire il log a un livello `DEBUG` ( `INFO` è impostato per impostazione predefinita)

## Problemi noti

None
