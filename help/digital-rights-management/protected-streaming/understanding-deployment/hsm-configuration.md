---
description: Se selezioni un HSM per memorizzare le credenziali del server, devi caricare le chiavi private e i certificati nell’HSM e creare un file di configurazione pkcs11.cfg.
title: Configurazione HSM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# Configurazione HSM{#hsm-configuration}

Se selezioni un HSM per memorizzare le credenziali del server, devi caricare le chiavi private e i certificati nell’HSM e creare un file di configurazione pkcs11.cfg.

È necessario individuare il file di configurazione nella directory *LicenseServer.ConfigRoot*.

Per un esempio di file di configurazione PKCS11, vedere la directory [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] sul DVD DRM di Adobe Primetime.

Consulta la documentazione del provider Sun PKCS11 relativa al formato del file [!DNL pkcs11.cfg] .

Puoi usare il seguente comando dalla directory in cui si trova il file [!DNL pkcs11.cfg] ( [!DNL keytool] è installato con Java JRE e JDK) per verificare che il file di configurazione HSM e Sun PKCS11 sia stato configurato correttamente:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se è possibile visualizzare le credenziali nell’elenco, l’HSM è configurato correttamente e il server licenze può ora accedere alle credenziali.
