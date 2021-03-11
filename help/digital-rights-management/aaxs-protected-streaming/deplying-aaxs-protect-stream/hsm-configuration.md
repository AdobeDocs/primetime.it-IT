---
title: Configurazione HSM
description: Configurazione HSM
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Configurazione HSM {#hsm-configuration}

Se scegli di utilizzare un HSM per memorizzare le credenziali del server, devi caricare le chiavi private e i certificati nell’HSM e creare un file di configurazione [!DNL pkcs11.cfg]. Questo file deve trovarsi nella directory *LicenseServer.ConfigRoot* . Per un esempio di file di configurazione PKCS11, vedere la directory [!DNL Adobe Access Server for Protected Streaming/configs] sul DVD Adobe Access. Per informazioni sul formato di [!DNL pkcs11.cfg], consulta la documentazione del provider Sun PKCS11.

Per verificare che il file di configurazione HSM e Sun PKCS11 sia configurato correttamente, è possibile utilizzare il seguente comando dalla directory in cui si trova il file [!DNL pkcs11.cfg] ( [!DNL keytool] è installato con Java JRE e JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se trovi le tue credenziali nell’elenco, l’HSM è configurato correttamente e il server delle licenze sarà in grado di accedere alle credenziali.

>[!NOTE]
>
>Adobe Access Server per lo streaming protetto non supporta attualmente gli HSM su sistemi operativi Windows a 64 bit.
