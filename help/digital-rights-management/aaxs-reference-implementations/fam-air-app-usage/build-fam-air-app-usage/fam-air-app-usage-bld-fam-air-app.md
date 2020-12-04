---
seo-title: Creazione dell'applicazione AIR di Gestione Flash Access
title: Creazione dell'applicazione AIR di Gestione Flash Access
uuid: 00927eb3-b8eb-4dd4-b528-91b70760c8cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Creazione dell&#39;applicazione AIR di Gestione Flash Access {#building-the-flash-access-manager-air-application}

Per creare il file AIR di Gestione Flash Access dal codice sorgente, è necessario che nel computer in uso sia installato Flex e AIR SDK. Prima di creare un pacchetto ed eseguire l&#39;applicazione, è necessario compilare il codice MXML in un file SWF utilizzando il compilatore [!DNL amxmlc]. Il compilatore [!DNL amxmlc] si trova nella directory [!DNL bin] dell&#39;SDK Flex 4 o successivo. Se lo desideri, puoi impostare la variabile di ambiente del percorso in modo che includa la directory bin dell’SDK per Flex per facilitare l’esecuzione delle utility dalla riga di comando.

Utilizzate la seguente procedura per creare il file AIR di Gestione Flash Access:

1. Aprite una shell comandi o un terminale e andate alla cartella di progetto dell&#39;applicazione AIR di Gestione Flash Access ( [!DNL UI Tools\Flash Access Manager] nella directory Implementazione di riferimento).
1. Digitate il comando seguente:

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   L&#39;esecuzione di [!DNL amxmlc] genera [!DNL FlashAccessManager.swf], che contiene il codice compilato dell&#39;applicazione.

 Adobe AIR SDK include l&#39;utility AIR Developer Tool (ADT) per creare pacchetti di applicazioni AIR e generare certificati. Le applicazioni AIR devono essere firmate digitalmente; gli utenti riceveranno un messaggio di avviso durante l&#39;installazione di applicazioni che non sono firmate correttamente o che non sono affatto firmate. Per generare un certificato utilizzando la riga di comando, aprite una finestra della console nella stessa cartella dell’applicazione AIR e digitate quanto segue:

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

Sostituire *some_password* con una password di vostra scelta. Dopo alcuni secondi, ADT deve completare il processo di generazione del certificato e si dovrebbe avere un nuovo file [!DNL testCert.pfx] nella directory dell&#39;applicazione.

Quindi, utilizzare ADT per creare un pacchetto dell&#39;applicazione in un file [!DNL .air], utilizzando il comando:

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

Questo comando indica ad ADT di creare il pacchetto dell&#39;applicazione, utilizzando il file chiave in [!DNL testCert.pfx]. Nella riga precedente, configurate ADT per creare il pacchetto dell&#39;intera applicazione in un file denominato [!DNL FlashAccessManager.air], e per includere i file [!DNL FlashAccessManager-app.xml] e [!DNL FlashAccessManager.swf] e le immagini dalla directory delle risorse.

Come parte di questa procedura, vi verrà richiesta la password impostata per il nuovo file di certificato. Inseritelo, attendete un momento e un file [!DNL FlashAccessManager.air] dovrebbe essere visualizzato nella stessa directory dei file di progetto.
