---
description: Se si seleziona un HSM per memorizzare le credenziali del server, è necessario caricare le chiavi private e i certificati nell'HSM e creare un file di configurazione pkcs11.cfg.
title: Configurazione HSM
exl-id: 4c4423ea-b7af-4a30-99ac-f5b74a1e1168
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Configurazione HSM{#hsm-configuration}

Se si seleziona un HSM per memorizzare le credenziali del server, è necessario caricare le chiavi private e i certificati nell&#39;HSM e creare un file di configurazione pkcs11.cfg.

È necessario individuare il file di configurazione nel *LicenseServer.ConfigRoot* directory.

Consulta la [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] sul DVD Adobe Primetime DRM per un file di configurazione PKCS11 di esempio.

Consultare la documentazione del provider Sun PKCS11 relativa al formato di [!DNL pkcs11.cfg] file.

È possibile utilizzare il seguente comando dalla directory in cui [!DNL pkcs11.cfg] il file si trova ( [!DNL keytool] viene installato con Java JRE e JDK) per verificare che il file di configurazione di HSM e Sun PKCS11 sia stato configurato correttamente:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se è possibile visualizzare le credenziali nell&#39;elenco, l&#39;HSM è configurato correttamente e il server licenze può ora accedere alle credenziali.
