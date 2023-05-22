---
title: Configurazione HSM
description: Configurazione HSM
copied-description: true
exl-id: 0418bcc1-0a85-4074-9616-915f77507bdd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Configurazione HSM {#hsm-configuration}

L&#39;utilizzo di un HSM non è richiesto, ma è raccomandato. L&#39;implementazione di riferimento può essere configurata per utilizzare il provider Sun PKCS11 per il supporto HSM. Per utilizzare una credenziale su un HSM, è necessario creare un file di configurazione per il provider Sun PKCS11. Per ulteriori informazioni, consultare la documentazione Sun. Per verificare che il file di configurazione di HSM e Sun PKCS11 sia configurato correttamente, è possibile utilizzare il seguente comando (keytool è installato con Java JDK):

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

Se le credenziali sono visualizzate nell’elenco, l’HSM è configurato correttamente.

>[!NOTE]
>
>A partire da Java 1.7, Sun Java per Windows a 64 bit non supporta le interfacce PKCS11 che Adobe Access DRM richiede per comunicare con i dispositivi HSM. Se prevedi di utilizzare un HSM, utilizza una versione a 32 bit di Java oppure un JDK che supporti l’intera interfaccia PKCS11.
