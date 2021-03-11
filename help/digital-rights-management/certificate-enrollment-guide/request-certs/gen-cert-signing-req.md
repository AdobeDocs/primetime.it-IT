---
title: Generare una richiesta di firma del certificato (Requester)
description: Generare una richiesta di firma del certificato (Requester)
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Generare una richiesta di firma del certificato (Requester) {#generate-a-certificate-signing-request-requester}

1. Genera una coppia di chiavi. Per utilizzare un&#39;utilità come OpenSSL, apri una finestra di comando e immetti quanto segue:

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >Adobe consiglia di includere il tipo di certificato (lic, pkgr, trans, trial o eval) nel nome della chiave. Questa convenzione di denominazione semplifica la distribuzione sul server licenze. In questo esempio viene utilizzato &quot;mycompany-license.key&quot;. Per le versioni di valutazione e valutazione, utilizza &quot;mycompany-eval.key&quot; e &quot;mycompany-trial.key&quot;.

1. Immetti una password per proteggere la chiave privata.

   Le password devono contenere almeno 12 caratteri. I caratteri devono includere una combinazione di caratteri e numeri ASCII maiuscoli e minuscoli. Per utilizzare OpenSSL per generare una password complessa, aprire una finestra di comando e immettere quanto segue:

   ```
   openssl rand -base64 8
   ```

1. Generare una richiesta di firma del certificato (CSR, Certificate Signing Request).

   Per utilizzare OpenSSL per generare una CSR, apri una finestra di comando e immetti quanto segue:

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. Viene richiesto di immettere la password per la chiave privata.
1. Crea una copia di backup della tua chiave privata e della tua password.

   Se perdi la chiave privata o se è compromessa, contatta l’amministratore del certificato di Adobe per revocare il certificato e richiederne una nuova.

   >[!NOTE]
   >
   >Adobe consiglia di utilizzare un HSM per proteggere la chiave privata e la password.

