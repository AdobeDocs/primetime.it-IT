---
seo-title: Creazione di un CRL CA per l'individuazione
title: Creazione di un CRL CA per l'individuazione
uuid: f722f3d1-517f-43e3-b892-f9287527fbe6
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Creazione di entità CA CRL{#create-individualization-ca-crl}

Questo punto di distribuzione Elenco revoca certificati (CRL) è incluso in ogni certificato computer emesso dal server di individualizzazione. Durante la convalida del certificato del computer sul server licenze, il CRL verrà scaricato dal punto di distribuzione elencato nel certificato (o letto dalla cache, se già scaricato) e controllato per verificare che il certificato non sia stato revocato.

>[!NOTE]
>
>Per impostare l&#39;URL per il punto di distribuzione CRL, è necessario impostare il campo [!DNL AdobeInitial.properties] `cert.machine.crldp`. Questo punto di distribuzione è *not* controllato da Primetime DRM per verificare la validità. È necessario verificare che questo URL sia valido. Gli errori risultanti da un URL non valido non saranno visibili fino a quando non verranno visualizzati errori di convalida dal server licenze.

Di seguito sono riportate istruzioni semplificate di esempio per l&#39;utilizzo di OpenSSL per creare CRL utilizzabili dal server licenze.  Adobe consiglia di eseguire questi passaggi in modo sicuro e in un ambiente, una volta ottenuta la credenziale CA Production Individualization CA.

1. Modificate la directory di lavoro nella directory [!DNL create_crl] inclusa in questa distribuzione.
1. Copiate la vostra scheda di identificazione CA [!DNL pfx] nella stessa directory [!DNL create_crl].

   I passaggi successivi presuppongono che il nome del file pfx della CA di individuazione sia [!DNL i15n.pfx]. Regolate le impostazioni in base alle vostre esigenze.
1. Estrarre la chiave privata del file CA di Individualizzazione [!DNL pfx].

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Convertite la chiave privata in formato [!DNL pksc8].

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Generare il CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   In questo esempio viene creato un CRL con un periodo di validità predefinito di 1 mese. Utilizzare le opzioni `-crldays` e `-crlhours` per ignorare i valori predefiniti.

   La generazione di un CRL utilizza il file [!DNL index] e [!DNL crlnumber] indicato nel [!DNL openssl.conf]. Per impostazione predefinita, viene utilizzata la posizione [!DNL demoCA] nella directory di lavoro. I file di esempio [!DNL index] e [!DNL crlnumber] sono inclusi nella directory [!DNL demoCA] fornita.

1. Distribuire il file CRL generato nel passaggio precedente in una posizione idonea raggiungibile dal server licenze (ad esempio: server di individualizzazione [!DNL ROOT]).
1. Riavviare il server licenze, una volta che il CRL è installato.
