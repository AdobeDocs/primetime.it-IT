---
title: Contenuto del pacchetto
description: Contenuto del pacchetto
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Contenuto del pacchetto{#packaging-content}

Quando si crea un pacchetto di contenuto, è necessario specificare l’URL del server licenze. L’URL Adobe Access Server ha il formato seguente:

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

Ad esempio, per il nome host del server licenze &quot;mylicenzieserver.com&quot; in ascolto sulla porta 8080 e un tenant denominato &quot;tenant1&quot;, l&#39;URL del server licenze da specificare al momento della creazione del pacchetto è:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Se ogni tenant utilizza un server licenze e credenziali di trasporto diverse, assicurati di specificare il certificato corretto del tenant nel packager.

Per garantire che il server rilasci le licenze solo per il contenuto in pacchetto da pacchetti noti, includi il certificato del packager nell&#39;elenco consentiti del packager del file di configurazione del tenant.
