---
seo-title: Creazione dell’applicazione AIR Flash Access Manager
title: Creazione dell’applicazione AIR Flash Access Manager
uuid: 00927eb3-b8eb-4dd4-b528-91b70760c8cd
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Creazione dell’applicazione AIR Flash Access Manager {#building-the-flash-access-manager-air-application}

Per creare il file AIR di Flash Access Manager dal codice sorgente, è necessario che Flex e AIR SDK siano installati nel computer. Prima di poter creare pacchetti ed eseguire l&#39;applicazione, è necessario compilare il codice MXML in un file SWF utilizzando il [!DNL amxmlc] compilatore. Il [!DNL amxmlc] compilatore si trova nella [!DNL bin] directory dell&#39;SDK Flex 4 o successivo. Se lo desiderate, potete impostare la variabile di ambiente del percorso in modo da includere la directory bin di Flex SDK per facilitare l&#39;esecuzione delle utility sulla riga di comando.

Per creare il file AIR di Flash Access Manager, effettuate le seguenti operazioni:

1. Aprite una shell dei comandi o un terminale e individuate la cartella di progetto dell’applicazione AIR Flash Access Manager ( [!DNL UI Tools\Flash Access Manager] nella directory Reference Implementation).
1. Digitate il comando seguente:

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   L&#39;esecuzione [!DNL amxmlc] produce [!DNL FlashAccessManager.swf], che contiene il codice compilato dell&#39;applicazione.

Adobe AIR SDK include l&#39;utility AIR Developer Tool (ADT) per creare pacchetti di applicazioni AIR e generare certificati. Le applicazioni AIR devono essere firmate digitalmente; gli utenti riceveranno un messaggio di avviso durante l&#39;installazione di applicazioni che non sono firmate correttamente o che non sono affatto firmate. Per generare un certificato utilizzando la riga di comando, aprite una finestra della console nella stessa cartella dell’applicazione AIR e digitate quanto segue:

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

Sostituire *some_password* con una password di vostra scelta. Dopo alcuni secondi, ADT dovrebbe completare il processo di generazione del certificato e dovreste avere un nuovo [!DNL testCert.pfx] file nella directory dell&#39;applicazione.

Quindi, utilizzate ADT per creare un pacchetto dell&#39;applicazione in un [!DNL .air] file, utilizzando il comando:

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

Questo comando indica ad ADT di creare il pacchetto dell&#39;applicazione, utilizzando il file chiave in [!DNL testCert.pfx]. Nella riga precedente, configurate ADT per creare un pacchetto dell’intera applicazione in un file denominato [!DNL FlashAccessManager.air], nonché per includere i file [!DNL FlashAccessManager-app.xml] e [!DNL FlashAccessManager.swf] le immagini presenti nella directory delle risorse.

Come parte di questa procedura, vi verrà richiesta la password impostata per il nuovo file di certificato. Inseritelo, attendete un momento e un [!DNL FlashAccessManager.air] file dovrebbe apparire nella stessa directory dei file di progetto.
