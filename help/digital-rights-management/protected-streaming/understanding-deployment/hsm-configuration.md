---
description: Se selezionate un HSM per memorizzare le credenziali del server, dovete caricare le chiavi private e i certificati nell'HSM e creare un file di configurazione pkcs11.cfg.
seo-description: Se selezionate un HSM per memorizzare le credenziali del server, dovete caricare le chiavi private e i certificati nell'HSM e creare un file di configurazione pkcs11.cfg.
seo-title: Configurazione HSM
title: Configurazione HSM
uuid: 3610840b-082e-4a73-8aa5-5065f9232e0b
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Configurazione HSM{#hsm-configuration}

Se selezionate un HSM per memorizzare le credenziali del server, dovete caricare le chiavi private e i certificati nell&#39;HSM e creare un file di configurazione pkcs11.cfg.

È necessario individuare il file di configurazione nella directory *LicenseServer.ConfigRoot*.

Per un esempio di file di configurazione PKCS11, vedere la directory [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] sul DVD DRM di Adobe Primetime .

Consultate la documentazione del provider Sun PKCS11 relativa al formato del file [!DNL pkcs11.cfg].

È possibile utilizzare il seguente comando dalla directory in cui si trova il file [!DNL pkcs11.cfg] ( [!DNL keytool] è installato con Java JRE e JDK) per verificare che il file di configurazione HSM e Sun PKCS11 sia stato configurato correttamente:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se è possibile visualizzare le credenziali nell&#39;elenco, l&#39;HSM è configurato correttamente e il server licenze può ora accedere alle credenziali.
