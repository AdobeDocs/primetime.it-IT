---
seo-title: Memorizzazione delle credenziali
title: Memorizzazione delle credenziali
uuid: a9e9db72-c921-4c28-ad1d-3fd3c2283f14
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Memorizzazione delle credenziali{#storing-credentials}

L&#39;SDK DRM di Primetime supporta diversi modi per memorizzare le credenziali, ad esempio utilizzando un modulo di sicurezza hardware (HSM) o come file PKCS12. L’SDK utilizza una credenziale (certificato di chiave pubblica e chiave privata associata) quando è richiesta la chiave privata. Ad esempio, il packager utilizza una credenziale per firmare i metadati; il server licenze utilizza una credenziale per decrittografare i dati crittografati con il server licenze o con la chiave pubblica Trasporto.

Per garantire la sicurezza del contenuto e del server licenze, dovete proteggere attentamente le chiavi private. PKCS12 è un formato di file di archivio standard per la memorizzazione delle credenziali crittografate con una password. Potete inoltre cifrare e firmare il file PKCS12 stesso. L&#39;estensione del file [!DNL .pfx] è comunemente utilizzata per i file che supportano questo formato.

>[!NOTE]
>
> Adobe consiglia di utilizzare un HSM per la massima sicurezza.
>
>Consultate la guida *alle linee guida* per la distribuzione protetta di Adobe Primetime DRM.

>[!NOTE]
>
>A partire da Java 1.7, Sun Java a 64 bit per Windows non supporta più le interfacce PKCS11 richieste da Primetime DRM per la comunicazione con i dispositivi HSM. Se si intende utilizzare un HSM, è necessario utilizzare una versione a 32 bit di Java, oppure un JDK che supporti le interfacce PKCS11 complete.

È possibile mantenere una chiave privata su un HSM e utilizzare Primetime DRM SDK per trasmettere la credenziale ottenuta dall’HSM. Se si desidera utilizzare una credenziale memorizzata in un HSM, è necessario utilizzare un provider JCE in grado di comunicare con un HSM per ottenere una maniglia per la chiave privata. Quindi dovete passare l&#39;handle di chiave privata, il nome del provider e il certificato a cui è inclusa la chiave pubblica a `ServerCredentialFactory.getServerCredential()`.

Il provider SunPKCS11 rappresenta un esempio di provider JCE che potete utilizzare per accedere a una chiave privata su un HSM. Alcuni HSM sono inclusi anche con un SDK Java fornito con un provider JCE.

Per istruzioni sull&#39;utilizzo di questo provider, consultate la documentazione di Sun Java.

PEM e DER sono metodi per codificare un certificato di chiave pubblica. PEM è una codifica base-64 e DER è una codifica binaria. I file di certificato in genere utilizzano l’estensione [!DNL .cer], [!DNL .pem]o [!DNL .der]. I certificati vengono utilizzati quando è richiesta solo una chiave pubblica. Se un componente richiede solo la chiave pubblica per funzionare, si consiglia di fornire al componente il certificato invece di un file di credenziali o PKCS12.
