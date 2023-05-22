---
title: Contenuto pacchetto
description: Contenuto pacchetto
copied-description: true
exl-id: 85950028-d58d-45b3-9337-9fcabe7cc4c0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# Contenuto pacchetto{#packaging-content}

Quando si crea un pacchetto di contenuto, è necessario specificare l&#39;URL del server licenze. L’URL di Adobe Access Server ha il formato:

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

Ad esempio, per il nome host del server licenze &quot;mylicenzieserver.com&quot; in ascolto sulla porta 8080 e un tenant denominato &quot;tenant1&quot;, l&#39;URL del server licenze da specificare al momento del packaging è:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Se ogni tenant utilizza un server licenze e credenziali di trasporto diverse, assicurarsi di specificare il certificato del tenant corretto nel packager.

Per garantire che il server emetta licenze solo per il contenuto collocato da package noti, includere il certificato del packager nell&#39;elenco consentiti del file di configurazione tenant.
