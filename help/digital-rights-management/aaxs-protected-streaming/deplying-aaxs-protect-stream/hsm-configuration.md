---
title: Configurazione HSM
description: Configurazione HSM
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Configurazione HSM {#hsm-configuration}

Se si sceglie di utilizzare un HSM per memorizzare le credenziali del server, è necessario caricare le chiavi private e i certificati nell&#39;HSM e creare un [!DNL pkcs11.cfg] file di configurazione. Questo file deve trovarsi nel file *LicenseServer.ConfigRoot* directory. Consulta la [!DNL Adobe Access Server for Protected Streaming/configs] sul DVD di Access di Adobe per un file di configurazione PKCS11 di esempio. Per informazioni sul formato di [!DNL pkcs11.cfg], consultare la documentazione del provider Sun PKCS11.

Per verificare che il file di configurazione di HSM e Sun PKCS11 sia configurato correttamente, è possibile utilizzare il comando seguente dalla directory in cui [!DNL pkcs11.cfg] il file si trova ( [!DNL keytool] è installato con Java JRE e JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se le credenziali sono visualizzate nell&#39;elenco, l&#39;HSM è configurato correttamente e il server licenze sarà in grado di accedere alle credenziali.

>[!NOTE]
>
>Adobe Access Server for protected Streaming non supporta attualmente gli HSM su sistemi operativi Windows a 64 bit.
