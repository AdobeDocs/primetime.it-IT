---
seo-title: Configurazione HSM
title: Configurazione HSM
uuid: da4d7118-65a8-460d-a796-b7bf5c28b208
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# Configurazione HSM {#hsm-configuration}

Se si sceglie di utilizzare un HSM per memorizzare le credenziali del server, è necessario caricare le chiavi private e i certificati nell&#39;HSM e creare un file di [!DNL pkcs11.cfg] configurazione. Questo file deve trovarsi nella directory *LicenseServer.ConfigRoot* . Per un esempio, consultate la [!DNL Adobe Access Server for Protected Streaming/configs] directory del DVD di Adobe Access. Per informazioni sul formato di [!DNL pkcs11.cfg], consultate la documentazione del fornitore Sun PKCS11.

Per verificare che il file di configurazione HSM e Sun PKCS11 sia configurato correttamente, potete utilizzare il seguente comando dalla directory in cui si trova il [!DNL pkcs11.cfg] file ( [!DNL keytool] è installato con Java JRE e JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se nell’elenco vengono visualizzate le credenziali, l’HSM è configurato correttamente e il server delle licenze sarà in grado di accedere alle credenziali.

> [!NOTE]
> Adobe Access Server per lo streaming protetto non supporta attualmente gli HSM nei sistemi operativi Windows a 64 bit.

