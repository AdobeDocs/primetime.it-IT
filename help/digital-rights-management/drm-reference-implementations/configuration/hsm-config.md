---
description: È possibile configurare l'implementazione di riferimento con il provider Sun PKCS#11 che supporta HSM. Sebbene non sia richiesto, l’uso di un HSM è consigliato.
title: Configurazione HSM
exl-id: 87a7d242-8202-4749-91a6-e6697be6a61d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Configurazione HSM{#hsm-configuration}

È possibile configurare l&#39;implementazione di riferimento con il provider Sun PKCS#11 che supporta HSM. Sebbene non sia richiesto, l’uso di un HSM è consigliato.

Per utilizzare una credenziale su un HSM, è necessario creare un file di configurazione per il provider Sun PKCS#11. Per ulteriori informazioni, vedere [Guida di riferimento di Java PCKS#11](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

Per verificare che il file di configurazione HSM e Sun PKCS#11 sia configurato, digitare il comando seguente utilizzando lo strumento chiave installato con Java JDK:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Hai configurato correttamente HSM se puoi visualizzare le tue credenziali nell’elenco.

>[!NOTE]
>
>A partire da Java 1.7, Sun Java per Windows a 64 bit non supporta più le interfacce PKCS#11 che Adobe Primetime DRM richiede per comunicare con i dispositivi HSM. Se prevedi di utilizzare un HSM, accertati di utilizzare una versione a 32 bit di Java o un JDK che supporti l’intera interfaccia PKCS#11.
