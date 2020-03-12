---
seo-title: Creazione di pacchetti di contenuto
title: Creazione di pacchetti di contenuto
uuid: 5d1d4b9d-f241-4291-9577-e9de5a8b92be
translation-type: tm+mt
source-git-commit: 47b2ed65ff0ea4f54a210cf7627ed535782296b9

---


# Creazione di pacchetti di contenuto{#packaging-content}

Quando create il pacchetto di contenuto, è necessario specificare l&#39;URL del server licenze. L&#39;URL di Adobe Access Server ha il formato seguente:

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

Ad esempio, per il nome host del server di licenze &quot;mylicenzieserver.com&quot; in ascolto sulla porta 8080 e un tenant denominato &quot;tenant1&quot;, l&#39;URL del server di licenze da specificare al momento della creazione del pacchetto è:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Se ogni tenant utilizza un server licenze e credenziali di trasporto diverse, accertatevi di specificare il certificato corretto del tenant nel packager.

Per garantire che il server rilasci le licenze solo per il contenuto incluso nei pacchetti da parte dei packager noti, includi il certificato del packager nella whitelist del file di configurazione del tenant.
