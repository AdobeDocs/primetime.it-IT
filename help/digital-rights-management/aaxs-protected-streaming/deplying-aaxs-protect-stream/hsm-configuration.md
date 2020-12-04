---
seo-title: Configurazione HSM
title: Configurazione HSM
uuid: da4d7118-65a8-460d-a796-b7bf5c28b208
translation-type: tm+mt
source-git-commit: ac75f63f98060e1937570476362bb5d4458d1f85
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Configurazione HSM {#hsm-configuration}

Se si sceglie di utilizzare un HSM per memorizzare le credenziali del server, è necessario caricare le chiavi private e i certificati nell&#39;HSM e creare un file di configurazione [!DNL pkcs11.cfg]. Questo file deve trovarsi nella directory *LicenseServer.ConfigRoot*. Per un esempio, vedere la directory [!DNL Adobe Access Server for Protected Streaming/configs] nel DVD di accesso al Adobe . Per informazioni sul formato di [!DNL pkcs11.cfg], consultate la documentazione del provider Sun PKCS11.

Per verificare che il file di configurazione HSM e Sun PKCS11 sia configurato correttamente, è possibile utilizzare il seguente comando dalla directory in cui si trova il file [!DNL pkcs11.cfg] ( [!DNL keytool] è installato con Java JRE e JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

Se nell’elenco vengono visualizzate le credenziali, l’HSM è configurato correttamente e il server delle licenze sarà in grado di accedere alle credenziali.

>[!NOTE]
>
> Adobe Access Server for protected Streaming non supporta attualmente gli HSM su sistemi operativi Windows a 64 bit.
