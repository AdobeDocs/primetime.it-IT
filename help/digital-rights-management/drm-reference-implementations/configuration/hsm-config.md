---
description: È possibile configurare l'implementazione di riferimento con il provider Sun PKCS#11 che supporta HSM. Anche se l’utilizzo di un HSM non è necessario, è consigliabile.
title: Configurazione HSM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Configurazione HSM{#hsm-configuration}

È possibile configurare l&#39;implementazione di riferimento con il provider Sun PKCS#11 che supporta HSM. Anche se l’utilizzo di un HSM non è necessario, è consigliabile.

Per utilizzare una credenziale su un HSM, è necessario creare un file di configurazione per il provider Sun PKCS#11. Per ulteriori informazioni, consulta la [Guida di riferimento di Java PCKS#11](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

Per verificare che il file di configurazione HSM e Sun PKCS#11 sia configurato, digitare il comando seguente utilizzando il keytool installato con Java JDK:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Hai configurato correttamente l’HSM se puoi visualizzare le tue credenziali nell’elenco.

>[!NOTE]
>
>A partire da Java 1.7, Sun Java per Windows a 64 bit non supporta più le interfacce PKCS#11 che Adobe Primetime DRM richiede per comunicare con i dispositivi HSM. Se prevedi di utilizzare un HSM, assicurati di utilizzare una versione a 32 bit di Java o di utilizzare un JDK che supporti l’interfaccia PKCS#11 completa.

