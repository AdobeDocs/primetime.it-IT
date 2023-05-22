---
title: Memorizzazione delle credenziali
description: Memorizzazione delle credenziali
copied-description: true
exl-id: ceb1bc19-56a0-47ce-affd-ce4ecb896c3b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Memorizzazione delle credenziali{#storing-credentials}

L’SDK di Primetime DRM supporta diversi modi per memorizzare le credenziali, incluso l’utilizzo di un modulo di sicurezza hardware (HSM) o come file PKCS12. L’SDK utilizza una credenziale (certificato a chiave pubblica e chiave privata associata) quando è richiesta la chiave privata. Ad esempio, il packager utilizza una credenziale per firmare i metadati; il server licenze utilizza una credenziale per decrittografare i dati che sono stati crittografati con il server licenze o la chiave pubblica di trasporto.

È necessario proteggere le chiavi private per garantire la sicurezza del contenuto e del server licenze. PKCS12 è un formato di file di archivio standard per l&#39;archiviazione delle credenziali crittografate con una password. È inoltre possibile crittografare e firmare il file PKCS12. Estensione del file [!DNL .pfx] viene comunemente utilizzato per i file che supportano questo formato.

>[!NOTE]
>
>L’Adobe consiglia di utilizzare un HSM per la massima sicurezza.
>
>Consulta la *Linee guida per l’implementazione sicura di Adobe Primetime DRM* guida.

>[!NOTE]
>
>A partire da Java 1.7, Sun Java per Windows a 64 bit non supporta più le interfacce PKCS11 che Primetime DRM richiede per la comunicazione con i dispositivi HSM. Se prevedi di utilizzare un HSM, devi utilizzare una versione a 32 bit di Java o un JDK che supporti le interfacce PKCS11 complete.

Puoi mantenere una chiave privata su un HSM e utilizzare l’SDK di Primetime DRM per passare le credenziali che ottieni da HSM. Se desideri utilizzare una credenziale memorizzata in un HSM, devi utilizzare un provider JCE in grado di comunicare con un HSM per ottenere un handle per la chiave privata. Quindi devi passare l’handle della chiave privata, il nome del provider e il certificato che include la chiave pubblica a `ServerCredentialFactory.getServerCredential()`.

Il provider SunPKCS11 rappresenta un esempio di provider JCE che è possibile utilizzare per accedere a una chiave privata su un HSM. Alcuni HSM sono inclusi anche in un SDK Java fornito in bundle con un provider JCE.

Per istruzioni su come utilizzare il provider, consultare la documentazione di Sun Java.

PEM e DER sono modi per codificare un certificato a chiave pubblica. PEM è una codifica base 64 e DER è una codifica binaria. I file di certificato utilizzano in genere l’estensione [!DNL .cer], [!DNL .pem], o [!DNL .der]. I certificati vengono utilizzati quando è richiesta solo una chiave pubblica. Se per il funzionamento di un componente è necessaria solo la chiave pubblica, è consigliabile fornire il certificato al componente anziché una credenziale o un file PKCS12.
