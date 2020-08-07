---
seo-title: Memorizzazione delle credenziali
title: Memorizzazione delle credenziali
uuid: dbce523c-32d9-423f-bc95-39786f85fc29
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Memorizzazione delle credenziali{#storing-credentials}

L’SDK supporta diversi metodi di memorizzazione delle credenziali (un certificato di chiave pubblica e la relativa chiave privata associata), incluso in un file HSM o PKCS12. Le credenziali vengono utilizzate quando è richiesta la chiave privata (ad esempio, per consentire al packager di firmare i metadati, o per consentire al server licenze di decrittografare i dati crittografati con la chiave pubblica License Server o Trasporto). Per garantire la sicurezza del contenuto e del server licenze, è necessario proteggere attentamente le chiavi private. PKCS12 è un formato standard per un file contenente una credenziale crittografata con una password. L&#39;estensione .pfx del file viene comunemente utilizzata per i file di questo formato.

>[!NOTE]
>
> Adobe consiglia di utilizzare un HSM per la massima sicurezza. Per ulteriori informazioni, vedere le Linee guida per l&#39;accesso sicuro agli Adobi .

>[!NOTE]
>
>A partire da Java1.7, Sun Java per Windows a 64 bit non supporta le interfacce PKCS11 che  Adobe Access DRM richiede per comunicare con i dispositivi HSM. Se intendete utilizzare un HSM, utilizzate una versione a 32 bit di Java o un JDK che supporti le interfacce PKCS11 complete.

È possibile mantenere una chiave privata in un modulo di protezione hardware (HSM) e utilizzare l’SDK per trasmettere la credenziale ottenuta dall’HSM. Per utilizzare una credenziale memorizzata in un HSM, utilizzare un provider JCE in grado di comunicare con un HSM per ottenere una handle per la chiave privata. Trasmettete quindi l’handle della chiave privata, il nome del provider e il certificato contenente la chiave pubblica in `ServerCredentialFactory.getServerCredential()`.

Il provider SunPKCS11 è un esempio di provider JCE che può essere utilizzato per accedere a una chiave privata su un HSM (consultate la documentazione di Sun Java per istruzioni sull&#39;utilizzo di questo provider). Alcuni HSM dispongono anche di un SDK Java che include un provider JCE.

PEM e DER sono due modi per codificare un certificato di chiave pubblica. PEM è una codifica base-64 e DER è una codifica binaria. I file di certificato in genere utilizzano le estensioni .cer, .pem. o .der. I certificati sono utilizzati in luoghi in cui è richiesta solo la chiave pubblica. Se un componente richiede solo la chiave pubblica per funzionare, è meglio fornire al componente il certificato invece di un file di credenziali o PKCS12.
