---
description: Quando si crea un pacchetto di contenuto, è necessario specificare l’URL del server licenze.
title: Contenuto del pacchetto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Contenuto del pacchetto{#packaging-content}

Quando si crea un pacchetto di contenuto, è necessario specificare l’URL del server licenze.

L&#39;URL del server DRM di Adobe Primetime utilizza il formato seguente:

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

Ad esempio, per il nome host del server di licenza `mylicenseserver.com` che ascolta la porta 8080 e un tenant denominato *`tenant1`*, è necessario utilizzare la sintassi seguente per l&#39;URL del server di licenze specificato al momento del package del contenuto:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Se ogni tenant utilizza un server licenze e credenziali di trasporto diverse, assicurati di specificare il certificato corretto del tenant nel packager.

Se si desidera assicurarsi che il server rilasci licenze solo per il contenuto dei pacchetti noti, è necessario includere il certificato del packager nell&#39;elenco consentiti del packager del file di configurazione del tenant.
