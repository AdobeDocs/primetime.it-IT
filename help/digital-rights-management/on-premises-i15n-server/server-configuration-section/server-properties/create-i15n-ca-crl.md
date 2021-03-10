---
title: Creare un CRL di CA per l'individuazione
description: Creare un CRL di CA per l'individuazione
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Crea Individuation CA CRL{#create-individualization-ca-crl}

Il punto di distribuzione dell’elenco di revoca dei certificati (CRL) è incluso all’interno di ogni certificato macchina rilasciato dal server di individualizzazione. Durante la convalida del certificato del computer sul server licenze, questo CRL verrà scaricato dal punto di distribuzione elencato nel certificato (o letto dalla cache se già scaricato) e controllato per verificare che il certificato non sia stato revocato.

>[!NOTE]
>
>Per impostare l’URL per il punto di distribuzione CRL, è necessario impostare il campo [!DNL AdobeInitial.properties] `cert.machine.crldp` . Questo punto di distribuzione è *non* controllato da Primetime DRM per la validità. Verifica che questo URL sia valido. Gli errori risultanti da un URL non valido verranno visualizzati solo dopo la visualizzazione degli errori di convalida dal server licenze.

Di seguito sono riportate le istruzioni semplificate, di esempio per l’utilizzo di OpenSSL per creare CRL utilizzabili dal server licenze. Adobe consiglia di eseguire questi passaggi in modo e in un ambiente sicuri, una volta ottenuta la credenziale Production Individualization CA.

1. Modifica la directory di lavoro nella directory [!DNL create_crl] inclusa in questa distribuzione.
1. Copia la CA di Individualizzazione [!DNL pfx] nella stessa directory [!DNL create_crl].

   I passaggi successivi presuppongono che Individualization CA pfx sia denominato [!DNL i15n.pfx]. Regolare in base alla configurazione.
1. Estrai la chiave privata del file Individualization CA [!DNL pfx].

   ```
   openssl pkcs12 -ini15n.pfx -nocerts -out i15n_priv.pem
   ```

1. Converti la chiave privata in formato [!DNL pksc8].

   ```
   openssl pkcs8 -topk8 -in i15n_priv.pem -inform pem -out i15n_pk8.pem -outform pem -nocrypt
   ```

1. Genera il CRL.

   ```
   openssl ca -keyform pem -keyfile ./i15n_pk8.pem -cert i15n.pem -gencrl  
     -out onprem-individualization -ca.crl
   ```

   In questo esempio viene creato un CRL con un periodo di validità predefinito di 1 mese. Utilizza le opzioni `-crldays` e `-crlhours` per sostituire i valori predefiniti.

   La generazione di un CRL utilizza il file [!DNL index] e [!DNL crlnumber] puntato nel [!DNL openssl.conf]. Per impostazione predefinita, viene utilizzata la posizione [!DNL demoCA] nella directory di lavoro. I file di esempio [!DNL index] e [!DNL crlnumber] sono inclusi nella directory [!DNL demoCA] fornita.

1. Distribuire il file CRL generato nel passaggio precedente in una posizione adeguata raggiungibile dal server licenze (ad esempio: server di individualizzazione [!DNL ROOT]).
1. Riavvia il server licenze una volta che il CRL è attivo.
