---
description: Quando create un pacchetto di contenuto, dovete specificare l'URL del server delle licenze.
seo-description: Quando create un pacchetto di contenuto, dovete specificare l'URL del server delle licenze.
seo-title: Creazione di pacchetti di contenuto
title: Creazione di pacchetti di contenuto
uuid: 2e47a9a2-bbc6-4995-8ce5-6ca6b116349b
translation-type: tm+mt
source-git-commit: 9d2e046ae259c05fb4c278f464c9a26795e554fc
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---


# Creazione di pacchetti di contenuto{#packaging-content}

Quando create un pacchetto di contenuto, dovete specificare l&#39;URL del server delle licenze.

L&#39;URL del server DRM di Adobe Primetime utilizza il formato seguente:

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

Ad esempio, per il nome host del server delle licenze `mylicenseserver.com` che ascolta sulla porta 8080 e un tenant chiamato *`tenant1`*, per l&#39;URL del server delle licenze utilizzate la sintassi seguente che avrete specificato al momento del pacchetto del contenuto:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

Se ogni tenant utilizza un server licenze e credenziali di trasporto diverse, accertatevi di specificare il certificato corretto del tenant nel packager.

Per essere certi che il server rilasci licenze solo per il contenuto dei packager noti, è necessario includere il certificato del packager nell&#39;elenco di consenti del file di configurazione tenant.
