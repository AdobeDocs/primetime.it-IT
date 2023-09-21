---
title: Conversione di file
description: Conversione di file
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---

# Conversione di file{#convert-files}

Utilizzando un’utility come OpenSSL e la chiave privata, il richiedente genera i file PKCS#12 (pfx) e PEM/DER immettendo i seguenti comandi da una finestra di comando:

1. Convertire il file PKCS#7 in un file PEM temporaneo.

   Per utilizzare OpenSSL, aprire una finestra di comando e immettere quanto segue:

   ```
   openssl pkcs7 -in mycompany-license.p7b -inform DER -out mycompany-license-temp.pem \ 
   -outform PEM -print_certs 
   ```

   >[!NOTE]
   >
   >Questo PEM temporaneo contiene il certificato e i certificati per le CA intermedie. Utilizzare questi certificati per generare il file PFX.

1. Convertire il file PEM temporaneo in un file PFX.

   Per utilizzare OpenSSL, aprire una finestra di comando e immettere quanto segue:

   ```
   openssl pkcs12 -export -inkey mycompany-license.key -in mycompany-license-temp.pem \ 
   -out mycompany-license.pfx -passin pass:private_key_password -passout pass:pfx_password 
   ```

1. Convertire il file PEM temporaneo in un file PEM finale.

   Per utilizzare OpenSSL, aprire una finestra di comando e immettere quanto segue:

   ```
   openssl x509 -in mycompany-license-temp.pem -inform PEM -out mycompany-license.pem -outform PEM 
   ```

   >[!NOTE]
   >
   >Anche se non obbligatorio, l’Adobe consiglia di utilizzare password diverse per la chiave privata (private_key_password) e la PFX (pfx_password).

   Il file PEM finale contiene solo il certificato.

1. Convertire il file PEM in un file DER.

   Per utilizzare OpenSSL, aprire una finestra di comando e immettere quanto segue:

   ```
   openssl x509 -in mycompany-license.pem -inform PEM -out mycompany-license.der -outform DER 
   ```

   >[!NOTE]
   >
   >I file DER sono necessari solo per il pacchetto HTTP Dynamic Streaming.
