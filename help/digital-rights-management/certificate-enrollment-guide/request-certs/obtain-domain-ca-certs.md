---
title: Ottieni certificati CA del dominio
description: Ottieni certificati CA del dominio
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Ottieni certificati CA di dominio{#obtain-domain-ca-certificates}

A differenza del certificato License Server, Packager o Transport, il certificato Domain CA non viene rilasciato da Adobe. Puoi ottenere questo certificato da un’autorità di certificazione oppure generare un certificato autofirmato da utilizzare a questo scopo.

Il certificato Domain CA deve utilizzare una chiave a 1024 bit e contenere gli attributi standard richiesti in un certificato CA:

* Estensione dei vincoli di base con il flag CA impostato su true
* Estensione Key Usage che specifica la firma del certificato è consentita

Ad esempio, utilizzando OpenSSL, è possibile generare un certificato CA autofirmato come segue:

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

