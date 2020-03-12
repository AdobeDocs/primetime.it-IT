---
seo-title: Configurazione HSM
title: Configurazione HSM
uuid: 1cc5be99-c24c-4c1e-9348-fb69f96d8ca5
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Configurazione HSM {#hsm-configuration}

L&#39;utilizzo di un HSM non è richiesto, ma è consigliato. L’implementazione di riferimento può essere configurata per utilizzare il provider Sun PKCS11 per il supporto HSM. Per utilizzare una credenziale su un HSM, è necessario creare un file di configurazione per il provider Sun PKCS11. Per informazioni, consulta la documentazione di Sun. Per verificare che il file di configurazione HSM e Sun PKCS11 sia configurato correttamente, potete utilizzare il seguente comando (keytool è installato con Java JDK):

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

Se nell’elenco vengono visualizzate le credenziali, l’HSM è configurato correttamente.

>[!NOTE] {class=&quot;- topic/note &quot;}
>
>A partire da Java 1.7, Sun Java per Windows a 64 bit non supporta le interfacce PKCS11 richieste da Adobe Access DRM per comunicare con i dispositivi HSM. Se intendete utilizzare un HSM, utilizzate una versione a 32 bit di Java o un JDK che supporti le interfacce PKCS11 complete.

