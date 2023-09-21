---
description: Quando si crea un pacchetto di contenuto, è necessario specificare l'URL del server licenze.
title: Contenuto pacchetto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# Contenuto pacchetto{#packaging-content}

Quando si crea un pacchetto di contenuto, è necessario specificare l&#39;URL del server licenze.

L&#39;URL del server Adobe Primetime DRM utilizza il seguente formato:

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

Ad esempio, per il nome host del server licenze `mylicenseserver.com` che ascolta sulla porta 8080 e un tenant denominato *`tenant1`*, è necessario utilizzare la sintassi seguente per l&#39;URL del server licenze specificato al momento della creazione del pacchetto del contenuto:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Se ogni tenant utilizza un server licenze e credenziali di trasporto diverse, verificare di specificare il certificato del tenant corretto nel packager.

Se si desidera assicurarsi che il server emetta licenze solo per il contenuto di package noti, è necessario includere il certificato del packager nell&#39;elenco consentiti del file di configurazione tenant.
