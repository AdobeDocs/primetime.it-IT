---
title: Ottenere certificati CA di dominio
description: Ottenere certificati CA di dominio
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Ottenere certificati CA di dominio{#obtain-domain-ca-certificates}

A differenza del certificato Server licenze, Packager o Trasporto, il certificato CA del dominio non viene rilasciato da Adobe. Puoi ottenere questo certificato da un’autorità di certificazione oppure generare un certificato autofirmato da utilizzare a questo scopo.

Il certificato CA del dominio deve utilizzare una chiave a 1024 bit e contenere gli attributi standard richiesti in un certificato CA:

* Estensione dei vincoli di base con il flag CA impostato su true
* L’estensione di utilizzo della chiave che specifica la firma del certificato è consentita

Ad esempio, utilizzando OpenSSL, è possibile generare un certificato CA autofirmato nel modo seguente:

1. Crea un file denominato [!DNL ca-extensions.txt] contenente:

   ```
   keyUsage=critical,keyCertSign  
   basicConstraints=critical,CA:TRUE  
   subjectKeyIdentifier=hash 
   ```

1. Genera chiave:

   ```
   openssl genrsa -des3 -out domain-ca.key 1024 
   ```

1. Genera CSR:

   ```
   openssl req -new -key domain-ca.key -out domain-ca.csr 
   ```

1. Genera certificato:

   ```
   openssl x509 -req -days 365 -in domain-ca.csr -signkey domain-ca.key \ 
     -out domain-ca.cer -extfile ca-extensions.txt 
   ```

1. Genera password:

   ```
   openssl rand -base64 8 
   ```

1. Genera PFX:

   ```
   openssl pkcs12 -export -inkey domain-ca.key \ 
   -in domain-ca.cer -out domain-ca.pfx
   ```
