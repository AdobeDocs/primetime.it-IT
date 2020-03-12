---
seo-title: Convertire i file
title: Convertire i file
uuid: e17ee003-5ac2-4bb8-83b7-81ee8fa9ee46
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# Convertire i file{#convert-files}

Utilizzando un’utility come OpenSSL e la chiave privata, il richiedente genera i file PKCS#12 (pfx) e PEM/DER immettendo i seguenti comandi da una finestra di comando:

1. Convertite il file PKCS#7 in un file PEM temporaneo.

   Per utilizzare OpenSSL, aprite una finestra di comando e immettete quanto segue:

   ```
   openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem \ 
   -outform PEM -print_certs 
   ```

   >[!NOTE]
   >
   >Questo PEM temporaneo contiene il certificato e i certificati per le CA intermedie. Utilizzate questi certificati per generare il file PFX.

1. Convertite il file PEM temporaneo in un file PFX.

   Per utilizzare OpenSSL, aprite una finestra di comando e immettete quanto segue:

   ```
   openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem \ 
   -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password 
   ```

1. Convertite il file PEM temporaneo in un file PEM finale.

   Per utilizzare OpenSSL, aprite una finestra di comando e immettete quanto segue:

   ```
   openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM 
   ```

   >[!NOTE]
   >
   >Sebbene non sia richiesto, Adobe consiglia di utilizzare password diverse per la chiave privata (private_key_password) e per PFX (pfx_password).

   Questo file PEM finale contiene solo il certificato.

1. Convertite il file PEM in un file DER.

   Per utilizzare OpenSSL, aprite una finestra di comando e immettete quanto segue:

   ```
   openssl x509 -in mycompany-license.pem -inform PEM -out mycompany-license.der -outform DER 
   ```

   >[!NOTE]
   >
   >I file DER sono richiesti solo per il packager di streaming HTTP dinamico.

