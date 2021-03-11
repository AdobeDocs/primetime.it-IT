---
title: Configurazione HSM
description: Configurazione HSM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---


# Configurazione HSM {#hsm-configuration}

L’utilizzo di un HSM non è necessario, ma è consigliato. L&#39;implementazione di riferimento può essere configurata per utilizzare il provider Sun PKCS11 per il supporto HSM. Per utilizzare una credenziale su un HSM, è necessario creare un file di configurazione per il provider Sun PKCS11. Per ulteriori informazioni, consulta la documentazione sul sole . Per verificare che il file di configurazione HSM e Sun PKCS11 sia configurato correttamente, è possibile utilizzare il seguente comando (keytool è installato con Java JDK):

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

Se trovi le tue credenziali nell’elenco, l’HSM è configurato correttamente.

>[!NOTE]
>
>A partire da Java 1.7, Sun Java per Windows a 64 bit non supporta le interfacce PKCS11 richieste da Adobe Access DRM per comunicare con i dispositivi HSM. Se prevedi di utilizzare un HSM, utilizza una versione a 32 bit di Java o utilizza un JDK che supporta l’interfaccia PKCS11 completa.

