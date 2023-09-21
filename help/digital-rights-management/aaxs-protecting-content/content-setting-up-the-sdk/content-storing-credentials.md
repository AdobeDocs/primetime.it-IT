---
title: Memorizzazione delle credenziali
description: Memorizzazione delle credenziali
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Memorizzazione delle credenziali{#storing-credentials}

L’SDK supporta diversi modi per archiviare le credenziali (un certificato a chiave pubblica e la relativa chiave privata associata), incluso su un HSM o come file PKCS12. Le credenziali vengono utilizzate quando è necessaria la chiave privata (ad esempio, per consentire al packager di firmare i metadati o al server licenze di decrittografare i dati crittografati con il server licenze o la chiave pubblica di trasporto). Le chiavi private devono essere protette per garantire la sicurezza del contenuto e del server licenze. PKCS12 è un formato standard per un file contenente credenziali crittografate utilizzando una password. L&#39;estensione .pfx è comunemente utilizzata per i file di questo formato.

>[!NOTE]
>
>L’Adobe consiglia di utilizzare un HSM per la massima sicurezza. Per ulteriori informazioni, consulta l’Adobe Linee guida per la distribuzione sicura degli accessi.

>[!NOTE]
>
>A partire da Java1.7, Sun Java per Windows a 64 bit non supporta le interfacce PKCS11 che Adobe Access DRM richiede per comunicare con i dispositivi HSM. Se prevedi di utilizzare un HSM, utilizza una versione a 32 bit di Java oppure un JDK che supporti l’intera interfaccia PKCS11.

È possibile mantenere una chiave privata in un modulo di sicurezza hardware (HSM) e utilizzare l&#39;SDK per passare le credenziali ottenute da HSM. Per utilizzare una credenziale archiviata in un HSM, utilizza un provider JCE in grado di comunicare con un HSM per ottenere un handle per la chiave privata. Quindi, passa l’handle della chiave privata, il nome del provider e il certificato contenente la chiave pubblica a `ServerCredentialFactory.getServerCredential()`.

Il provider SunPKCS11 è un esempio di provider JCE che può essere utilizzato per accedere a una chiave privata su un HSM (per istruzioni sull&#39;utilizzo di questo provider, vedere la documentazione di Sun Java). Alcuni HSM sono dotati anche di un SDK Java che include un provider JCE.

PEM e DER sono due modi per codificare un certificato a chiave pubblica. PEM è una codifica base 64 e DER è una codifica binaria. I file di certificato utilizzano in genere l’estensione .cer, .pem. o .der. I certificati vengono utilizzati in luoghi in cui è richiesta solo la chiave pubblica. Se un componente richiede solo la chiave pubblica per funzionare, è meglio fornire a tale componente il certificato anziché le credenziali o il file PKCS12.
