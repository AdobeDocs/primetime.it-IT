---
seo-title: Generazione di una richiesta di firma del certificato (richiedente)
title: Generazione di una richiesta di firma del certificato (richiedente)
uuid: 04abd5d2-77ac-4f89-8bea-31d389159aee
translation-type: tm+mt
source-git-commit: b4b50471ab0ba98329862322a61bf73aa9e471d5

---


# Generazione di una richiesta di firma del certificato (richiedente) {#generate-a-certificate-signing-request-requester}

1. Genera una coppia di chiavi. Per utilizzare un&#39;utilità come OpenSSL, apri una finestra di comando e immetti quanto segue:

   ```
   openssl genrsa -des3 -out mycompany-license.key 1024
   ```

   >[!NOTE]
   >
   >Adobe consiglia di includere il tipo di certificato (ad esempio, pkgr, trans, versione di prova o eval) nel nome della chiave. Questa convenzione di denominazione semplifica la distribuzione dei nomi nel server licenze. In questo esempio viene utilizzato &quot;mycompany-license.key&quot;. Per le versioni di valutazione e prova, utilizzate &quot;mycompany-eval.key&quot; e &quot;mycompany-trial.key&quot;.

1. Immettete una password per proteggere la chiave privata.

   Le password devono contenere almeno 12 caratteri. I caratteri devono includere una combinazione di caratteri ASCII maiuscoli e minuscoli e numeri. Per utilizzare OpenSSL per generare una password complessa, aprite una finestra di comando e immettete quanto segue:

   ```
   openssl rand -base64 8
   ```

1. Generare una richiesta di firma dei certificati (CSR).

   Per utilizzare OpenSSL per generare un CSR, aprite una finestra di comando e immettete quanto segue:

   ```
   openssl req -new -key mycompany-license.key -out mycompany-license.csr -batch 
   ```

1. Viene richiesto di immettere la password per la chiave privata.
1. Crea una copia di backup della tua chiave privata e della password.

   Se perdete la chiave privata o se questa è compromessa, contattate l&#39;amministratore di certificati Adobe per revocare il certificato e richiederne uno nuovo.

   >[!NOTE]
   >
   >Adobe consiglia di utilizzare un HSM per proteggere la chiave privata e la password.

