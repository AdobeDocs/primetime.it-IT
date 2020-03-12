---
seo-title: Creazione di un CRL CA per l'individuazione
title: Creazione di un CRL CA per l'individuazione
uuid: f722f3d1-517f-43e3-b892-f9287527fbe6
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Creazione di un CRL CA per l&#39;individuazione{#create-individualization-ca-crl}

Questo punto di distribuzione Elenco revoca certificati (CRL) è incluso in ogni certificato computer emesso dal server di individualizzazione. Durante la convalida del certificato del computer sul server licenze, il CRL verrà scaricato dal punto di distribuzione elencato nel certificato (o letto dalla cache, se già scaricato) e controllato per verificare che il certificato non sia stato revocato.

>[!NOTE]
>
>Per impostare l&#39;URL per il punto di distribuzione CRL, è necessario impostare il [!DNL AdobeInitial.properties] campo `cert.machine.crldp` . Questo punto di distribuzione *non* viene controllato dalla DRM di Primetime per verificare la validità. È necessario verificare che questo URL sia valido. Gli errori risultanti da un URL non valido non saranno visibili fino a quando non verranno visualizzati errori di convalida dal server licenze.

Di seguito sono riportate istruzioni semplificate di esempio per l&#39;utilizzo di OpenSSL per creare CRL utilizzabili dal server licenze. Adobe consiglia di eseguire questi passaggi in modo e in un ambiente sicuri, una volta ottenuta la credenziale Production Individualization CA.

1. Modificate la directory di lavoro nella [!DNL create_crl] directory inclusa in questa distribuzione.
1. Copiate l&#39;API di Individualizzazione [!DNL pfx] nella stessa [!DNL create_crl] directory.

   Nei passaggi successivi si presuppone che sia denominato Individualization CA pfx [!DNL i15n.pfx]. Regolate le impostazioni in base alle vostre esigenze.
1. Estrarre la chiave privata del [!DNL pfx] file CA di Individualizzazione.

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Converti la chiave privata in [!DNL pksc8] formato.

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Generare il CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   In questo esempio viene creato un CRL con un periodo di validità predefinito di 1 mese. Utilizzate le opzioni `-crldays` e `-crlhours` per ignorare i valori predefiniti.

   La generazione di un CRL utilizza il [!DNL index] file e il [!DNL crlnumber] file a cui si punta nel [!DNL openssl.conf]. Per impostazione predefinita, viene utilizzata la [!DNL demoCA] posizione nella directory di lavoro. Esempio [!DNL index] e [!DNL crlnumber] file sono inclusi nella [!DNL demoCA] directory fornita.

1. Distribuire il file CRL generato nel passaggio precedente in una posizione idonea raggiungibile dal server licenze (ad esempio: server di individualizzazione [!DNL ROOT]).
1. Riavviare il server licenze, una volta che il CRL è installato.
