---
title: Creazione dell'applicazione AIR Flash Access Manager
description: Creazione dell'applicazione AIR Flash Access Manager
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# Creazione dell&#39;applicazione AIR Flash Access Manager {#building-the-flash-access-manager-air-application}

Per creare il file AIR di Flash Access Manager dal codice sorgente, è necessario che Flex e AIR SDK siano installati nel computer. Prima di creare un pacchetto ed eseguire l&#39;applicazione, è necessario compilare il codice MXML in un file SWF utilizzando il compilatore [!DNL amxmlc]. Il compilatore [!DNL amxmlc] si trova nella directory [!DNL bin] dell&#39;SDK Flex 4 o successivo. Se lo desideri, puoi impostare la variabile dell&#39;ambiente del percorso in modo da includere la directory bin dell&#39;SDK Flex per facilitare l&#39;esecuzione delle utility sulla riga di comando.

Utilizza la seguente procedura per creare il file AIR di Flash Access Manager:

1. Apri una shell di comando o un terminale e passa alla cartella di progetto dell’applicazione AIR Flash Access Manager ( [!DNL UI Tools\Flash Access Manager] nella directory Implementazione di riferimento).
1. Immetti il seguente comando:

   ```
   amxmlc src\FlashAccessmanager.mxml
   ```

   L&#39;esecuzione di [!DNL amxmlc] produce [!DNL FlashAccessManager.swf], che contiene il codice compilato dell&#39;applicazione.

L’SDK di Adobe AIR include l’utility AIR Developer Tool (ADT) per la creazione di pacchetti di applicazioni AIR e la generazione di certificati. Le applicazioni AIR devono essere firmate digitalmente; gli utenti riceveranno un avviso durante l’installazione di applicazioni che non dispongono di una firma adeguata o che non dispongono di alcuna firma. Per generare un certificato utilizzando la riga di comando, apri una finestra della console nella stessa cartella dell’applicazione AIR e digita quanto segue:

```
adt -certificate -cn SelfSigned 1024-RSA testCert.pfx  
<i class="+ topic ph hi-d="" i "="">
  some_password 
</i class="+ topic>
```

Sostituisci *some_password* con una password di tua scelta. Dopo alcuni secondi, ADT deve completare il processo di generazione del certificato e dovresti avere un nuovo file [!DNL testCert.pfx] nella directory dell&#39;applicazione.

Quindi, utilizza ADT per creare un pacchetto dell&#39;applicazione in un file [!DNL .air], utilizzando il comando:

```
adt -package -storetype pkcs12 -keystore testCert.pfx FlashAccessManager.air src\FlashAccessManager-app.xml . -C src assets
```

Questo comando comunica ad ADT di creare un pacchetto dell&#39;applicazione utilizzando il file chiave in [!DNL testCert.pfx]. Nella riga precedente, configura ADT per creare un pacchetto dell’intera applicazione in un file denominato [!DNL FlashAccessManager.air], e per includere i file [!DNL FlashAccessManager-app.xml] e [!DNL FlashAccessManager.swf] e le immagini dalla directory delle risorse.

Come parte di questa procedura, ti verrà richiesta la password impostata per il nuovo file di certificato. Inseriscilo, attendi un attimo e un file [!DNL FlashAccessManager.air] dovrebbe apparire nella stessa directory dei file di progetto.
