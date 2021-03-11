---
title: Memorizzazione delle credenziali
description: Memorizzazione delle credenziali
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Memorizzazione delle credenziali{#storing-credentials}

L’SDK supporta diversi modi per memorizzare le credenziali (un certificato a chiave pubblica e la relativa chiave privata associata) , anche in un file HSM o PKCS12. Le credenziali vengono utilizzate quando è richiesta la chiave privata (ad esempio, affinché il gestore di pacchetti firmi i metadati o per il server licenze decrittografi i dati crittografati con il server licenze o con la chiave pubblica di trasporto). Le chiavi private devono essere protette in modo da garantire la sicurezza del contenuto e del server licenze. PKCS12 è un formato standard per un file contenente una credenziale crittografata utilizzando una password. L&#39;estensione file .pfx viene comunemente utilizzata per i file di questo formato.

>[!NOTE]
>
>Adobe consiglia di utilizzare un HSM per la massima sicurezza. Per ulteriori informazioni, consulta le linee guida per la distribuzione sicura dell’accesso Adobe .

>[!NOTE]
>
>A partire da Java1.7, Sun Java per Windows a 64 bit non supporta le interfacce PKCS11 richieste da Adobe Access DRM per comunicare con i dispositivi HSM. Se prevedi di utilizzare un HSM, utilizza una versione a 32 bit di Java o utilizza un JDK che supporta l’interfaccia PKCS11 completa.

È possibile mantenere una chiave privata in un modulo HSM (Hardware Security Module) e utilizzare l&#39;SDK per passare la credenziale ottenuta dall&#39;HSM. Per utilizzare una credenziale memorizzata in un HSM, utilizza un provider JCE in grado di comunicare con un HSM per ottenere un handle alla chiave privata. Quindi, passa l&#39;handle di chiave privata, il nome del provider e il certificato contenente la chiave pubblica a `ServerCredentialFactory.getServerCredential()`.

Il provider SunPKCS11 è un esempio di provider JCE che può essere utilizzato per accedere a una chiave privata su un HSM (consulta la documentazione Sun Java per istruzioni sull&#39;utilizzo di questo provider). Alcuni HSM sono inoltre dotati di un SDK Java che include un provider JCE.

PEM e DER sono due modi per codificare un certificato a chiave pubblica. PEM è una codifica base-64 e DER è una codifica binaria. I file di certificato in genere utilizzano l’estensione cer, pem. o .der. I certificati vengono utilizzati in posizioni in cui è richiesta solo la chiave pubblica. Se un componente richiede solo la chiave pubblica per funzionare, è meglio fornire al componente il certificato invece di un file di credenziali o PKCS12.
