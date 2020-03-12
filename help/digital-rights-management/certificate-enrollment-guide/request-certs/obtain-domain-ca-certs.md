---
seo-title: Ottenere i certificati CA del dominio
title: Ottenere i certificati CA del dominio
uuid: 41bbe02b-363a-47f4-9cc0-350730b6c787
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# Ottenere i certificati CA del dominio{#obtain-domain-ca-certificates}

A differenza del certificato License Server, Packager o Transport, il certificato Domain CA non viene emesso da Adobe. È possibile ottenere questo certificato da un&#39;autorità di certificazione oppure generare un certificato autofirmato da utilizzare a tale scopo.

Il certificato Domain CA deve utilizzare una chiave a 1024 bit e contenere gli attributi standard richiesti in un certificato CA:

* Estensione Vincoli di base con il flag CA impostato su true
* Estensione dell&#39;uso chiave che specifica che la firma del certificato è consentita

Ad esempio, utilizzando OpenSSL, è possibile generare un certificato CA autofirmato come segue:

1. Create un file denominato [!DNL ca-extensions.txt] contenente:

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

