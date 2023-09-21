---
title: Genera una richiesta di firma del certificato (richiedente)
description: Genera una richiesta di firma del certificato (richiedente)
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Genera una richiesta di firma del certificato (richiedente) {#generate-a-certificate-signing-request-requester}

1. Genera una coppia di chiavi. Per utilizzare una utility come OpenSSL, aprire una finestra dei comandi e immettere quanto segue:

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >L’Adobe consiglia di includere il tipo di certificato (lic, pkgr, trans, trial o eval) nel nome della chiave. Questa convenzione di denominazione semplifica la distribuzione sul server licenze. In questo esempio viene utilizzato &quot;mycompany-license.key&quot;. Per le versioni di valutazione e prova, utilizza &quot;mycompany-eval.key&quot; e &quot;mycompany-trial.key&quot;.

1. Immettere una password per proteggere la chiave privata.

   Le password devono contenere almeno 12 caratteri. I caratteri devono includere una combinazione di caratteri ASCII maiuscoli e minuscoli e numeri. Per utilizzare OpenSSL per generare una password sicura, aprire una finestra di comando e immettere quanto segue:

   ```
   openssl rand -base64 8
   ```

1. Genera una richiesta di firma del certificato (CSR, Certificate Signing Request).

   Per utilizzare OpenSSL per generare una CSR, aprire una finestra di comando e immettere quanto segue:

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. Viene richiesto di immettere la password per la chiave privata.
1. Crea una copia di backup della chiave privata e della password.

   Se la chiave privata viene persa o compromessa, contatta l’amministratore dei certificati Adobe per revocare il certificato e richiederne uno nuovo.

   >[!NOTE]
   >
   >L’Adobe consiglia di utilizzare un HSM per proteggere la chiave privata e la password.
