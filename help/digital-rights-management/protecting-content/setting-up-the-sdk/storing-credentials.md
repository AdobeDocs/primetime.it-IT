---
title: Memorizzazione delle credenziali
description: Memorizzazione delle credenziali
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# Memorizzazione delle credenziali{#storing-credentials}

L&#39;SDK DRM di Primetime supporta diversi modi per memorizzare le credenziali, tra cui l&#39;utilizzo di un modulo di sicurezza hardware (HSM) o come file PKCS12. L’SDK utilizza una credenziale (certificato a chiave pubblica e chiave privata associata) quando è richiesta la chiave privata. Ad esempio, il packager utilizza una credenziale per firmare i metadati; il server licenze utilizza una credenziale per decrittografare i dati crittografati con il server licenze o la chiave pubblica di trasporto.

Per garantire la sicurezza del contenuto e del server licenze, è necessario proteggere strettamente le chiavi private. PKCS12 è un formato di file di archivio standard per l&#39;archiviazione delle credenziali crittografate con una password. (È inoltre possibile crittografare e firmare il file PKCS12 stesso.) L’estensione del file [!DNL .pfx] viene comunemente utilizzata per i file che supportano questo formato.

>[!NOTE]
>
>Adobe consiglia di utilizzare un HSM per la massima sicurezza.
>
>Consulta la guida *Adobe Primetime DRM Secure Deployment Guidelines* .

>[!NOTE]
>
>A partire da Java 1.7, Sun Java per Windows a 64 bit non supporta più le interfacce PKCS11 richieste da Primetime DRM per la comunicazione con i dispositivi HSM. Se si intende utilizzare un HSM, è necessario utilizzare una versione a 32 bit di Java o un JDK che supporti l&#39;interfaccia PKCS11 completa.

Puoi mantenere una chiave privata in un HSM e utilizzare l’SDK DRM di Primetime per passare la credenziale ottenuta dall’HSM. Se desideri utilizzare una credenziale memorizzata in un HSM, devi utilizzare un provider JCE in grado di comunicare con un HSM per ottenere un handle per la chiave privata. Quindi devi passare l’handle di chiave privata, il nome del provider e il certificato che include la chiave pubblica a `ServerCredentialFactory.getServerCredential()`.

Il provider SunPKCS11 rappresenta un esempio di provider JCE che è possibile utilizzare per accedere a una chiave privata in un HSM. Alcuni HSM sono anche inclusi con un SDK Java fornito con un provider JCE.

Per istruzioni su come utilizzare questo provider, consulta la documentazione di Sun Java .

PEM e DER sono modi per codificare un certificato a chiave pubblica. PEM è una codifica base-64 e DER è una codifica binaria. I file di certificato in genere utilizzano l’estensione [!DNL .cer], [!DNL .pem] o [!DNL .der]. I certificati vengono utilizzati quando è richiesta solo una chiave pubblica. Se un componente richiede solo la chiave pubblica per funzionare, è consigliabile fornire al componente il certificato invece di un file di credenziali o PKCS12.
