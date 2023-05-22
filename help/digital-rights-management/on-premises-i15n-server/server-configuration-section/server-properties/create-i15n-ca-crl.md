---
title: Crea CRL CA di personalizzazione
description: Crea CRL CA di personalizzazione
copied-description: true
exl-id: 72147209-1337-4aed-9e4e-210c905c55a4
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Crea CRL CA di personalizzazione{#create-individualization-ca-crl}

Questo punto di distribuzione CRL (Certificate Revocation List) è incluso in ogni certificato del computer rilasciato dal server di individuazione. Durante la convalida del certificato del computer sul server licenze, questo CRL verrà scaricato dal punto di distribuzione elencato nel certificato (o letto dalla cache se è già stato scaricato) e selezionato per verificare che il certificato non sia stato revocato.

>[!NOTE]
>
>Per impostare l&#39;URL del punto di distribuzione CRL, è necessario impostare [!DNL AdobeInitial.properties] `cert.machine.crldp` campo. Questo punto di distribuzione è *non* verifica della validità da parte di DRM Primetime. Verifica che questo URL sia valido. Gli errori derivanti da un URL non valido non saranno visibili finché non verranno visualizzati errori di convalida dal server licenze.

Di seguito sono riportate istruzioni semplificate e di esempio per l’utilizzo di OpenSSL per creare CRL utilizzabili dal server licenze. L’Adobe consiglia di eseguire questi passaggi in modo sicuro e in un ambiente sicuro, una volta ottenute le credenziali CA di Production Individualization.

1. Cambiate la directory di lavoro in [!DNL create_crl] directory inclusa in questa distribuzione.
1. Copia la tua CA di Personalizzazione [!DNL pfx] allo stesso [!DNL create_crl] directory.

   I passaggi successivi presuppongono che il nome del file pfx della CA di personalizzazione sia [!DNL i15n.pfx]. Adatta in base alla configurazione.
1. Estrarre la CA di personalizzazione [!DNL pfx] chiave privata del file.

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Converti la chiave privata in [!DNL pksc8] formato.

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Genera il CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   Questo esempio crea un CRL con un periodo di validità predefinito di 1 mese. Utilizza il `-crldays` e `-crlhours` opzioni per sostituire i valori predefiniti.

   La generazione di un CRL utilizza [!DNL index] e [!DNL crlnumber] file indicato nel tuo [!DNL openssl.conf]. Per impostazione predefinita, il [!DNL demoCA] viene utilizzata la posizione nella directory di lavoro. Esempio [!DNL index] e [!DNL crlnumber] i file sono inclusi nel [!DNL demoCA] directory.

1. Distribuire il file CRL generato nel passaggio precedente in una posizione appropriata raggiungibile dal server licenze (ad esempio, server di personalizzazione) [!DNL ROOT]).
1. Riavviare il server licenze una volta che il CRL è attivo.
