---
description: Potete configurare l’implementazione di riferimento con il provider Sun PKCS#11 che supporta HSM. Anche se l'uso di un HSM non è richiesto, è consigliato.
seo-description: Potete configurare l’implementazione di riferimento con il provider Sun PKCS#11 che supporta HSM. Anche se l'uso di un HSM non è richiesto, è consigliato.
seo-title: Configurazione HSM
title: Configurazione HSM
uuid: 2741ac40-aa42-4aa7-9864-037f3ed3dee2
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---


# Configurazione HSM{#hsm-configuration}

Potete configurare l’implementazione di riferimento con il provider Sun PKCS#11 che supporta HSM. Anche se l&#39;uso di un HSM non è richiesto, è consigliato.

Per utilizzare una credenziale su un HSM, è necessario creare un file di configurazione per il provider Sun PKCS#11. Per ulteriori informazioni, consultare la Guida di riferimento di [Java PCKS#11](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

Per verificare che il file di configurazione HSM e Sun PKCS#11 sia configurato, digitare il comando seguente utilizzando lo strumento chiave installato con Java JDK:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

L&#39;HSM è stato configurato correttamente se è possibile visualizzare le credenziali nell&#39;elenco.

>[!NOTE]
>
>A partire da Java 1.7, Sun Java per Windows a 64 bit non supporta più le interfacce PKCS#11 che  Adobe Primetime DRM richiede di comunicare con i dispositivi HSM. Se intendete utilizzare un HSM, assicuratevi di utilizzare una versione a 32 bit di Java o un JDK che supporti le interfacce PKCS#11 complete.

